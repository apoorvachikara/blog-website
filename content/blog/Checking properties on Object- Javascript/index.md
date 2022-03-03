---
title: Checking properties in Object - Javascript
date: "2022-03-03T03:12:03.284Z"
description: "How to check the properties added to the objects? Why do we need to use in-built object methods?"
---

<img src="./js-object-props.png" alt="imagenode" style="width:200px;"/>

## Introduction

We have been dealing with objects on every line when we write javascript code and Of course adding the keys is really an elementary operation we do on objects in Javascript. I have seen even the experience developer `not using` **Object.hasOwnProperty** method to check if the object has the provided property.

And this is the reason I come up with another blog so we can see when to use what.

### Why do we need it?

In JS, objects have been created from Object class and has a lot of properties to it. How we have all the properties because of the inheritance. 

```
const obj = {};
console.log(obj['toString']); // it prints the function definition
```

When we run the above code, you get the function definition printed on the console. Why? It is an empty object. This is the how JS objects are created and how can you check all the properties inherited from Object global class.

```
const obj = {};
console.log(obj['toString']); // it prints the function definition
console.dir(obj); // you can check all the properties
```

Now, you can check all the properties inherited from Prototype of Object. When we do `Object['key']` or `in`, it checks all the properties in prototype chain.

### Object['key'] vs Object.hasOwnProperty

Although `Object['key']` is a lookup in the object, we know object is the Hash table and Big O(1) for every key lookup if it exists. But what if the properties don't exist, it checks in the object and it's prototype chain.

So, when we need to actually get the exclusive property on object, we should use `Object.hasOwnProperty` and it only checks if the property is only a part of the given object.


### Interview Questions

1. Properties defined by user on below object like `status`:

```
const obj = {
    URL: "avtechtechstand.web.app",
    status: "running"
}
```

So, you need to use `Object.hasOwnProperty` to check if the property exist on object or not. Even if it doesn't exist you need to use it just to confine your check with in object itself and avoid prototype chaining if you can. 

2. How do you find property original in the below code?

```
function foo() {}
foo.prototype.original = 'Parent Value';

function bar() {}
const proto = { extended_original: 'Child Value' };

Object.setPrototypeOf(proto, foo.prototype);
bar.prototype = proto;

const instance_check = new bar();
console.log(instance_check.original);
console.log(instance_check.extended_original);
```

Now, if you check `instance_check.hasOwnProperty('original')` it o/ps `false`. So how do you check if the property really exist - check with  `instance_check['original']` and it will display **the value** if it exists else **undefined**.