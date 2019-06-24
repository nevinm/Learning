# Learning
Random finds

Async await through loops testing: (https://lavrton.com/javascript-loops-how-to-handle-async-await-6252dd3c795/)

```
function delay() {
  return new Promise(resolve => setTimeout(resolve, Math.random()*1000));
}

async function delayedLog(item) {
  // notice that we can await a function
  // that returns a promise
  await delay();
  console.log(item);
}
```

Concurrent process - Will not wait to finish. (forEach/map)
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
o/P: Done!
5
2
6
3
7
4
1
```


Sequentially waiting to finish:

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
o/P: 1
2
3
4
5
6
7
Done!
```


Wait for everything to finish:
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
O/P: 7
4
3
5
6
1
2
Done!
```
