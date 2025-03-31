# code
- [await-in-loop](#await-in-loop)
  
<br>

## Await Loop

<a href="#await-in-loop"><img align="right" width="15" height="15" src="https://git.io/JtehR" alt="Back to top"></a>

<details><summary>await-in-loop</summary>
https://eslint.org/docs/latest/rules/no-await-in-loop
```js
  const f1 = () => {
    return new Promise((resolve, reject) => {
      setTimeout(() => {
        console.log(1)
        resolve('one')
      }, 5000)
    })
  }

  const f2 = () => {
    return new Promise((resolve, reject) => {
      setTimeout(() => {
        console.log(2)
        reject('error two')
      }, 2000)
    })
  }
  
  const f3 = () => {
    return new Promise((resolve, reject) => {
      setTimeout(() => {
        console.log(3)
        resolve('three')
      }, 3000)
    })
  }

  f1().then(res => console.log(res))
  f2().then(res => console.log(res))
  f3().then(res => console.log(res))

  const  queuePromise = async(arr) => {
    return await  arr.reduce((acc,current) => {
      return acc.then(current)
    }, Promise.resolve())
  }

  queuePromise([f1(), f2(), f3()])
  
  async function processArray(array) {
    for (const item of array) {
      await item
    }
  }

  processArray([f1(), f2(), f3()])
  
  async function processArray() {
    let res = Promise.resolve();
    const result = [];
  
    res = await f1();
    result.push(res)
    res = await f2();
    result.push(res)
    res = await f3();
    result.push(res)
  
    console.log(result)
  }

  processArray();
  
  async function foo(things) {
    const promises = [];
    for (const thing of things) {
      promises.push(thing);
    }
  
      const results = await Promise.all(promises);
      return results;
  }
  
  const res = foo([f1(), f2(), f3()])
  
  res.then(res => console.log(res))
     .catch(e => console.log(e))
```
</details>
