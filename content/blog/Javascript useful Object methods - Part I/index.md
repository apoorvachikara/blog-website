---
title: Javascript Object methods - Part 1
date: "2022-04-05T03:12:03.284Z"
description: "Almost everything is object in Javascript and there are plenty of methods on object class. Whenever the new object is created, all these methods are accessible on the new object."
---

<img src="./intro.png" alt="imagenode" style="width:200px;"/>

## Introduction

Object is one of the data types in JavaScript. It is a key-value data store and can be build using object class constructor, object literals, object initializer. If you want to check types in JS, you can check [Types In Javascript](/Types%20in%20JS/).

Let's see how can we create objects in JS:

```
const obj_1 = {name: "Apoorva Chikara"}; // {name: 'Apoorva Chikara'}
const obj_2 = new Object({name: "Apoorva Chikara"}); //{name: 'Apoorva Chikara'}
const obj_3 = Object.create({}, { name: {value: "Apoorva Chikara", writable: true }}); //{name: 'Apoorva Chikara'}
```

Of course, all the object produces same o/p then why do we three different methods to achieve the same o/p? What we see as the o/p is same in all the cases, however, things under the hood are very different. We will discuss these scenarios later in the blog. 

But before we proceed, let's talk about how many properties, methods and static methods are present on Object class.

- Object.assign()
- Object.create()
- Object.defineProperties()
- Object.defineProperty()
- Object.entries()
- Object.freeze()
- Object.isFrozen()
- Object.seal()
- Object.isSealed()
- Object.preventExtensions()
- Object.isExtensible()
- Object.getOwnPropertyNames()
- Object.getOwnPropertySymbols()
- Object.hasOwnProperty()
- Object.keys()
- Object.values()

There are a few others that I will add in the series of blog because it will be difficult to understand a lot stuff at one go.

## Object.assign()

This method allows to copy all the enumerable properties from one to multiple source objects. You can see the syntax below:

```
Object.assign(targetObejct, sourceObject1, sourceObject2..., sourceObjectN);
```

Example: person is the target object and return as modified object 

```
const person = {fname: "Apoorva"};
const personAge = {age: 30};
const personLastName = {lname: "Chikara"};

Object.assign(person, personFirstName, personAge, personLastName);
console.log(person) // {fname: 'Apoorva', age: 30, lname: 'Chikara'}
```

### In-depth 

- It is only used to copy enumerable properties from the object for its own properties. You can't copy properties from its prototype. 

- It invokes getter and setters on source and target object respectively.

- You can clone the objects i.e you can copy them, but it doesn't allow deep copy(only shallow copy).

```
const obj1 = {a: 1111};
const obj2 = Object.assign({}, obj1);

```

- You can use it to merge objects

```
const obj1 = {a: 1};
const obj2 = {b: 2};
const obj3 = {c: 3};
Object.assign({}, obj1, obj2, obj3); // {a: 1, b: 2, c: 3}
```


## Object.create()

As the name suggests, we can create a new object using this method. Isn't is `{}` can be used to create a new one? Well, yes, but this creates a new object from the prototype of existing object.



### In-depth

`Object.create(proto, propertiesObject)` - It asks the `proto` form which it has to create a new object. The proto has to be `null` or an `object`, you can't use primitive types here.

```
const obj = Object.create(null);
console.log(obj) // {}
```
When you check the `obj` will be null and you won't be seeing any methods or properties in obj because it has taken prototype of null that doesn't hold any methods.

```
console.log(`convert` + obj) // Error: Cannot convert object to primitive value
```

It means you can't access any methods on the obj. So, when you create an object always provide the correct `proto` from where you cant to create the object from. It is mainly used to create new objects from the existing prototype.

## Object.defineProperty()

It is a static method and used to define new property or update the existing one.

```
const obj = {name: "foo"};
Object.defineProperty(obj, 'second Name', {writable: true, enumerable: true, value: 'bar'});
console.log(obj) // {name: 'foo', second Name: 'bar'}
```

As you see, we have added the property to the `obj`. You can also use this method to update the property.

### In-depth

- When you call the method with default value, you won't be able to modify the key i.e not immutable and enumerable.

- Property descriptors comes into two types: data descriptors and accessor descriptor.

- Data descriptors is property with value assigned to it.

```
const obj = {};
Object.defineProperty(obj, 'URL', {value: "https://avtechstand.web.app/", writable: true, configurable: false});
console.log(obj) // {'URL' : "https://avtechstand.web.app/"}
```

- Accessor descriptors is the property assigned with getter and setter functions. 

```
let newValue = 1111
const obj = {};
Object.defineProperty(obj, 'key', {
    get() {return newValue},
    set(value1) { newValue = value1},
    enumerable: true
})
console.log(obj) // try running it.
```

- You can't add both the descriptors to define a single property. It will throw a type error `Invalid property descriptor`.

```
let newValue = 1111
const obj = {};
Object.defineProperty(obj, 'key', {
    get() {return newValue},
    set(value1) { newValue = value1},
    enumerable: true,
    value: 34
})
```

## Object.defineProperties()

It is similar to the above method, but can help us to assign number of properties in one go. 

```
const obj = {};
Object.defineProperties(obj, {
    'name' : {
        value: "Apoorva Chikara"
    }, 
    'city' : {
        value: 'Noida' 
    }
})
```

The only thing that matters is you provide the keys in the form of an object and its data or accessor configuration as the value to the key your are adding

**Note: I will add the remaining methods and properties in the upcoming blogs**

## Interview Questions

1) What will be the o/p of below code?

```
const ob1 = null;
const ob2 = 1;
const ob3 = true;
Object.assign({}, ob1, ob2, ob3); // {}
```

```
const ob1 = "null";
const ob2 = 1;
const ob3 = true;
Object.assign({}, ob1, ob2, ob3); // {"0": "n", "1":"u", "2": "l", "3": "l"}
```

The reason is when we can assign on the source object they are first converted to objects instead of primitives. Then there values are assigned to the target object. 

First case, `null` will be ignored `1` and `true` will be converted to `new Number(1)` and `new Boolean(true)` by calling toObject method. It will return nothing as value so nothing will be assigned to target object.

Second case, when `toObject` is called on string `new String('null')`, it will return the enumerable string - like this `0: "a", 1: "b", 2: "c"`. So it will be assigned to target object.

2) what is the difference in the below code?

```
const obj = {};
obj['name'] = "Apoorva Chikara"

const obj = {};
const value = 'Apoorva Chikara'
Object.defineProperty(obj, 'name', {value});
```

The difference is that first property will be iterated and by default `configurable`, `writable` and `enumerable`. However, the second one is not. So, when you want to make the property configurable use Object.defineProperty.

3) what is the o/p of the code and how can you fix it?

```
const obj = Object.create(null);
obj.toString();
```

This is what we can do:

```
const obj = Object.create(null);
obj.toString = toString;
obj.toString();
```

Since, the new object doesn't have this method as copied from null prototype that has no methods. We copy it from the generic version.

```
const obj = Object.create(null);
Object.setPrototypeOf(obj, Object.prototype)
obj.toString = toString;
obj.toString();
```

Note: if you want to contribute, please check the [github](https://github.com/apoorvachikara/blog-website)
