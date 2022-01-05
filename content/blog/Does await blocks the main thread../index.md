---
title: Does async/await blocks the main thread?
date: "2022-01-01T22:12:03.284Z"
description: "Learn Autoboxing to understand how primitives type access methods and properties."
---

### Introduction async/await

These days, the websites are becoming more interactive. It has become increasingly important to do cpu-intensive operations like encryption, fectching large data from APIs by making external calls, etc. We have different things to handle distinct operations - encryption can be handled on web workers, APIs calls can be handled asynchronously (there are others things to cover, will do that in subsequent blogs).  

As Javascript is single-threaded programming language, we won't discuss how it handle all the operations. We will discuss about async/await. It is a syntactic sugar on promises. A lot of developers are using async/await without knowing the underlying process of how they actually works. I have been seeing a lot of question on stackoverflow realting to their usage and does they actually block the main thread?

This is quiet strange we use await to make the function synchronous(really!!) i.e we can control the flow or can hold the flow of execution where we use the await keyword provided that async should be placed for JS interperter(**later version of JS does allow await keyword usage without async i.e at the top level**); 

### When to use?

Async/await uses promises under the hood and when we should use promises? If there is any async operations that suceeds or fails in near future. Earlier we uses callbacks and they created the callback hell when nesting them. 

So, we started to use promises that can be cascased using then/catch. However, some developers still prefer to write async code with synchronous style and ***ECMAScript 2016(ES7)*** introduced ***async functions*** and ***await keyword*** to make working easier with promises.

```
// run this code in the broswer
// see what is the o/p and why?


const asycnBlock2 = () => {
  return new Promise((res, rej) => {
         setTimeout(() =>{
               res('It will be resolved');
         }, 1000)
  });
}

const asycnBlock3 = () => {
  return new Promise((res, rej) => {
     setTimeout(() =>{
               res('It will be rejected');
         }, 2000);

  })
}

const asycnBlock1 = async () => {
    try {
       const result = await asycnBlock2();
       const result2 = await asycnBlock3();
       console.log(`It won't be printed until await is resolved`);
       console.log(`Result: ${result}, Result2: ${result2}`);
    } catch (e) {
       console.log(`This will be printed on any rejection`)
       console.log(`Error is ${e.message}`);
    }
}


await asycnBlock1();

console.log('Blocking the main thread?');
```

### Working

How does it actually work? So, I am adding a simple async/await code and try to explain how javascripts executes it.

```
const wait = (time) => new Promise((res, rej) => setTimeout(() => res(`I have waited ${time} before executing this statement`),time));
const main = async () => {
    try {
        const result = await wait(4000);
        console.log(result);
    } catch (e) { console.log(e) };
}

main();
```
When we run the above code, we can see the results won't be printed until wait resolves or rejects (for this specific example if resolves). Javascript basically interprets it like a then and catchable series of statements. 

```
const wait = (time) => new Promise((res, rej) => setTimeout(() => res(`I have waited ${time} before executing this statement`),time));
const main = async () => {
    return new Promise((res, rej) => {
          wait().then((result) =>  {
            console.log(result);
            res(result)
            }).catch(e =>  console.log(e));
    });
}

main();
```

The above code o/p the exact same results, this is how Javascript reads the above async/await code and execute it.

### Myths?

Does it blocks the main thread? As Javascript is single threaded language and anything that blocks the main thread will hamnper the user experience and if running on Node.js will impact the exection of business logic. So, how does it actually handles it without blocking the main thread? 

From the above code, we have seen how async/await is just a wrapper or syntactic sugar on the promises. It very well explains how Javascript pushes things on the event loop to execute it. 



### Interview Questions

1) 


