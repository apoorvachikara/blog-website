---
title: Types in Javascript
date: "2021-12-10T22:12:03.284Z"
description: "Understanding types in JS is one of the fundamental concepts. You will be ready to answer any `types` based questions after reading this blog. Please leave your comments on github if you feel any information is incorrect."
---

Javascript is a dynamically typed language and most people do not think it has types. All programming languages have some built-in types and data structures. In this article, I will attempt to cover the types and related interview questions. 

When we talk about a **dynamically typed language**, **JS** is one of the first languages that comes to mind. Of course there are a lot of others too, but we will be focusing on JS only. 

Variables are not directly assigned to any specific type, and any variable can be assigned or reassigned values of all types, you are not bound to any specific type. Following are the examples:

``` 
let foo = “bar”;
foo = 29;
foo = undefined  
```

All these statements are valid in the JS context. However, it is important to know what types are being natively defined by the language. Having a thorough understanding of each type and their behavior is extremely essential to convert values to different types, it is known as coercion(will be covered in its own blog). 

## Javascript Types primitive and object

There are built-in types provided by the language and it is called primitive types. However, it is feasible to create some types using a **new** operator which becomes the object, we will be discussing it after a few paragraphs. 

        null
        undefined
        boolean
        number
        string
        bigint
        symbol (ES6 onwards)

All these types are called primitives and you can use **typeof** operator to inspect the type of any value which returns any one of the seven values specificed above. 

**Note** : All types except objects define immutable values (that is, values which can't be changed).

```
typeof undefined // “undefined”
typeof “hello world” // “string”
typeof 1111 // number
typeof false // boolean
typeof {“foo” : “bar”} // “object”
typeof BigInt(1234) // “bigint”
typeof Symbol() // “symbol”
```

You might have noticed why I haven’t included the type null in the above examples because its *special*. 

```
typeof null // “object” → why is that!!!
```

If it is a primitive type, it should have returned *null*? This is a bug in JS, yes, and it has been there for more than two decades and seems will never be fixed. A lot of web software might be dependent on this and it will create a lot more bugs. So, how do we check if the value is null or not?

```
let a = null;
if (!a && typeof a === “object”) console.log(`Yes, ${a} is null!`);
```
Note: **null** is the only primitive type which is falsy(it is evaluated false in conditions), but returns as “object”. I will cover falsy and truthy values later in this blog

**Objects** are collections of key/values pairs. The keys should be strings even if you use number/boolean it will be parsed to string(toString is called) and the values can be of any type mentioned above or objects. You can access value using '.'/dot operator or object['key'].

```
const obj = {'foo': 'bar', true: 'false', 1: 'numeric value'};
obj.foo // bar
obj.true // false
obj.1 // it will be an error --> Uncaught SyntaxError: Unexpected number
```
Why the last one is throwing an error if all the keys are parsed to strings? Because numbers can't be a valid variable name, converting number to string will allow accessing the value. You can check this [stackoverflow](https://stackoverflow.com/questions/8698792/javascript-object-key-beginning-with-number-allowed) link for more details.

```
const obj = {'foo': 'bar', true: 'false', "1": 'numeric value'};
obj.foo // bar
obj.true // false
obj["1"] // numeric value
```

## Interview questions on Types

1) What is the o/p of the below code?
    
		
		typeof typeof false // “string”
		
When we run first **typeof**, it returns the value **'boolean'**. Now, the ypeof 
 **'boolean'** will return string as it is quoted in the string(typeof return value is of type 
string).

2) What is the o/p of the below code?

		
		typeof NaN // “number”
		typeof infinity // “number”
		typeof [1, 2, 4] // “object”
		 
	
    - The first one is a property NaN(Not a Number), it is returned when converting any invalid number(ex +“3a” will return NaN). You can also check Number.IsNaN(value), itreturns boolean value.

	- The second one is **Infinity**. This property is on global object represent numeric infinity. So it return **”number”** as type

	- The Third one is an array. When we check the typeof array, it returns object which is correct as arrays are objects in JS(not only arrays everything is object). If you want to check if an object is an array there could be different ways, one of those is using a method on Array class. **Array.isArray([1, 2, 3])**. This will return value in boolean either **true/false**.

3) What is the o/p of the below code?

	
			let func = () => {};
			typeof func; // “function”

Why? “function”!!! , it should return “object” as functions are first class objects. There is no such type in JS. So, the main reason to provide it is to provide some helpful specification to the developers (do let me know if you find a more verbose answer).


