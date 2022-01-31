---
title: Javascript Useful Array Methods
date: "2022-01-05T22:12:03.284Z"
description: "Useful array methods in Javascript. Learn when to use them and what does they return?"
---


There are many methods that are added in the Array class that is a part of a global object. We have been using arrays almost every day. The question is when to use what method on arrays. How to use them efficiently, when to use what method? This blog will help you understand them in-depth and will also clear up some myths.

Also, I am adding **what do they return when we call them ?**  

### List of methods

1) forEach
2) map 
3) filter
4) push
5) pop
6) at


### forEach

This is an array method that helps to iterate through an array and executes the function passed to it on every element. 

```
const arr = [1, 2, 3, 4];
arr.forEach(el => {
      // do anything 
    console.log(el);
})
```

It doesn't return anything instead write to the console as we passed it to the function.

```
const arr = [1, 2, 3, 4];

function updateCurrentArray (element, index, array, this) {
       array[index] = element * 2;
}

arr.forEach(updateCurrentArray);
console.log(arr); // you will see the update values
```

You can replace `for` loop with `forEach`, however, there is an argument that `for` loop is efficient ([for vs forEach](https://stackoverflow.com/questions/43031988/javascript-efficiency-for-vs-foreach)).

You can't use `forEach` for promises, you can't break them or stop them like `for` loops. The range of elements processed by forEach() is set before the first invocation of callback Functions. 

#### When to use forEach

You can replace it with for loop, it's easy to read and you don't need to set up a lot of things for it as we have in `for` loops. In simple terms, forEach is a general array tool and can be used when we won't be able to use any other method.


## map

It is useful when you want to create a new array populated with the results get from the callback function on every element.

```
const numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
const squares = numbers.map(x => x*2);
console.log(squares);
```

Here, we will be getting a new array in squares. The callback function will be called on every element even it doesn't have values. It won't call the callback function on indexes that are not set or deleted indexes.

```
const arr = [1, 2, 3, 4];
delete arr[2];
arr.map(x => x * 2); // return the array [2, 4, empty, 10]
```
`map` is also immutable as it won't impact the array it is running on. It is also **chainable** as it returns the array. The range of elements processed by map() is set before the first invocation of callback Functions. 

#### When not to use map

1) You are not returning values from the callback.
2) You are not using the returned array.


## filter

As the name suggests, it helps to filter out the element from the array that matches a specific condition. The callback function runs on every element, but the returned array will only contain those elements from the array that passes the condition.

```
const numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
const even = numbers.filter(x => x % 2 === 0);
console.log(even); // [2, 4, 6, 8, 10]
```

`filter` doesn't mutate the array on which it is called. The range of elements processed by filter() is set before the first invocation of callback Functions.

By default the filter method not passes the `empty` or `zero` values in the callback i.e it should `truthy` to pass the condition.

#### When to use filter

There can be many use cases, but you should use it when you want to find out elements based on some condition/s and you can use the returned values.


## push/pop

`push` and `pop` methods are used to add and remove elements from the array tail. You can add multiple elements to the array using `push` and it **returns the new length of an array** on which it is called.

```
const arr = [99, 100, 101];
arr.push(...[102, 103]); // 5
```

`pop` is used to remove an element from the tail of an array and **returns** the value itself. What happens if you pass any number to the pop method? Well, it can accept any arguments, but won't take them into account and **always return the last element value**.

```
const arr = [99, 100, 101];
arr.pop(...[102, 103]); // 101
```

#### When to use push and pop

I think it is quite straightforward to understand when to use them. We don't need any specific scenarios.

## at

It is a simple method introduced to find the value at the given index. It accepts the integer values positive and negative. If we pass a negative value it calculates from the last element in the array.

```
const arr = [99, 100, 101, 102, 103];
arr.at(2) // 101
arr.at(-7) // undefined
arr.at(-2) // 102
```

When the index is greater than the array length or lesser than the array length(negative values), it will print undefined.

#### When to use at

You can't use **negative index** to access the index using square brackets, but it can help to achieve this.

## Interview Questions

1) What will be the o/p for the below code?

```
const arr = [1, 2, 3, 4, , 6];
arr.forEach(el => console.log(el));
```

It won't run the callback function for empty indexes and even for the deleted ones (try it in console, you will find it). 

2) Does `forEach` mutates the array called on?

No, It doesn't. We call the callback function on every element. Depending upon the callback function we can say for ex:

```
const arr = [1, 2, 3, 4];
arr.forEach((el , index, array) => {
     array[index] = el * 2;
})
```

This code does mutate it because we are doing that else it will run the logic on every element.

3) Can we call `filter` on `map`?

Yes, we can do that as these methods are chainable and we can run other available methods on the returned array. We can chain only those methods that return an array.

4) What is the o/p of below code?

```
const arr = [1, 2, ,3];
arr.filter(x => x === x);
```

The o/p is `[1, 2, 3]` because the filter cb only passes the values to the result if they are `truthy` in nature.
