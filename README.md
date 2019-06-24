# Learning
Random finds

## Async await through loops testing: (https://lavrton.com/javascript-loops-how-to-handle-async-await-6252dd3c795/)

```
function delay() {
  return new Promise(resolve => setTimeout(resolve, Math.random()*1000));
}

async function delayedLog(item) {
  console.log(`Started with item ${item}`);
  // notice that we can await a function
  // that returns a promise
  await delay();
  console.log(item);
}
```

## Concurrent process - Will not wait to finish. (forEach/map)
```
async function processArray(array) {
  array.forEach(async (item) => {
    await delayedLog(item);
  })
  console.log('Done!');
}

processArray([1, 2, 3, 4, 5, 6, 7]);
```

```
o/P:
Started with item 1
Started with item 2
Started with item 3
Started with item 4
Started with item 5
Started with item 6
Started with item 7

Done!
5
2
6
3
7
4
1
```


## Sequentially waiting to finish: (for of/for loop)

```
async function processArray(array) {
  for (const item of array) {
    await delayedLog(item);
  }
  console.log('Done!');
}
processArray([1, 2, 3, 4, 5, 6, 7]);
```
```
o/P: 
Started with item 1
1
Started with item 2
2
Started with item 3
3
Started with item 4
4
Started with item 5
5
Started with item 6
6
Started with item 7
7
 Done!
```

## Waits for everything to finish:
```
async function processArray(array) {
  // map array to promises
  const promises = array.map(delayedLog);
  // wait until all promises are resolved
  await Promise.all(promises);
  console.log('Done!');
}
processArray([1, 2, 3, 4, 5, 6, 7]);
```

```
O/P: 
Started with item 1
Started with item 2
Started with item 3
Started with item 4
Started with item 5
Started with item 6
Started with item 7
Promise {<pending>}
7
5
6
2
4
3
1
Done!
```
