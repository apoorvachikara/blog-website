---
title: AutoBoxing in Javascript
date: "2021-12-20T22:12:03.284Z"
description: "Learn Autoboxing to understand how primitives type access methods and properties."
---

Autoboxing in Javascript is not a new topic, but most of us have not heard or learned about it. Have you ever wondered why primitive types are able to access their associated object properties or methods? 

If you want to know about types, I have a very descriptive blog [here](/Types%20in%20JS/). You can excel on **types in 2 minutes** in Javascript.


### Primitives Types

Creating a string and checking its length will be an easy task, but how string primitive type is able to access the property on the String object?

```
const foo = "bar";
console.log(foo.length); // 3
```

**Primitive types** don't have any properties and methods on them. From the above code, it seems the primitives do have methods on it, but this is not the case here. It's magic and we can it an autoboxing feature in JS. 


Whenever we call any method or property on primitive types, the primitives are wrapped into their associative objects(i.e built-in objects). In the above case, it is a string. So, **autoboxing** helps connect primitive types to their built-in objects and provides methods and properties to access on it.

There are a few cases, I would like to showcase first then we will discuss them.



|S.no.| code   |      output      |
|:----|:----------|:-------------:|
|1| String('hello')|  'hello' |
|2| String('hello') == new String('hello') |    true   |
|3| String('hello') === new String('hello')  | false |
|4| new String('hello') === new String('hello') |    false   |
|5| new String('hello') == new String('hello')  | false |
|6| String('hello') instanceof String     |    false   |
|7| new String('hello') instanceof String   | true |
    

 1. It is a string primitive and when you console it, it returns the value which is being passed.

 2. This is a comparison operation b/w string primitive and string object(it is created when call using new). As this will only compare the values, the returned o/p is true. But if you check the `new String('hello world')` output, What do you see in the console?

 3. Here we are checking the values with type and definitely it will return false as types are different. One is `string` and the other is `object`.

 4. Why it is `false`? We are comparing objects and two different objects can't be the same even if they have the same values, Why? Because they are compared by reference(i.e their memory address and it will be different for every object), this is the reason for `false`.

 5. Again, it has the same explanation as above. The object holds the memory address as the value in it which refers to the exact values it holds in it(Know about pointers? if not check [this](https://stackoverflow.com/questions/518000/is-javascript-a-pass-by-reference-or-pass-by-value-language#:~:text=It's%20always%20pass%20by%20value,persist%20outside%20of%20the%20function.)).

 6. As the string is a primitive type, it is not an instance of the String class. However to access property autoboxing is done.

 7. Since it is created using the `new` operator it is an instance of the String class.

### When and Why use primitives?
Generally, we should use primitives when we are using strings, numbers or any primitive types. It is efficient and why is that? 

```
const testStr = "Hello world!";
console.log(testStr.valueOf());
```

The above string is primitive and it doesn't have any method and properties attached to it. So, the value of `testStr` will be accessed with a much higher speed. In the next statement, what happens when we fetch the values of length properties? Since `testStr` is not an instance of string, JS will auto-box it by checking the type and aligning with the same wrapper to it. 

JS calls like this `testStr.valueOf().prototype.toString.call = [object String]`, it is done back and forth based on the methods we are calling on primitive type. These days the JS engines are pretty advanced and it is not necessary that the above-mentioned process will be held every time. 

### Interview Question 

1. Difference b/w String() and new String()?

You can't add properties to string primitive, however you can do that when you create it using new.

```
let testStr = 'Hello World';
testStr = "Hello World Updated"; // new string will be constructed they are immutable

// with new String()
let testStr = new String('Hello World');
testStr = "Hello World Updated"; // updates the same object testStr
```

2. How can we make the below statement true?

```
String('hello') === new String('hello');
```
We know that this will return false, but how can we actually access the values of the string object? You can use the `valueOf` method and it will return the values of the object be it String, Number or boolean.

```
String('hello') === new String('hello').valueOf();
```




