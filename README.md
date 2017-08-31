# Creating Objects

## Objectives
+ Create a constructor function
+ Use a constructor function to create an object
+ Explain what a constructor function is and how it works
+ Explain what `this` is in the context of an object

## Introduction

So far we have mainly examined primitive data types like strings and integers.  As you have seen, it sometimes becomes convenient to represent data with objects, which gives us key value pairs. For example, we may represent a puppy as the following:

```javascript
  let puppy = {name: 'fido', age: 2, color: 'brown'}

  // our JavaScript object
````

Now imagine that we had a couple of puppies:

```js
let fido = {
  name: 'fido',
  age: 2,
  color: 'brown',
  size: 'large'
}

let pluto = {
  name: 'pluto',
  age: 3,
  color: 'yellow',
  size: 'medium'
}

```

Great. Two nice puppies.

Note, that with a both objects sharing exactly the same keys, and only the values differing, we are *[repeating ourselves](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself)*.  We would like a mechanism to construct objects with the same attributes (that is, keys), while assigning different values to those keys.   

### Constructor Function

Instead of typing out each attribute separately with the literal syntax, we can use a *constructor function*.  It operates as a factory for new objects.

Let's write a constructor function that returns a Javascript object without any attributes:

```js
function Puppy() {

}

Puppy()
// undefined


new Puppy
// {}
```

Let's unpack the code above.  First, we declare a function called `Puppy`.  We capitalize the name of the function simply as a convention, to indicate that we will be using this function differently.  This function is just a plain old JavaScript function.  We demonstrate that by calling `Puppy()` and seeing that it returns undefined, just like any other blank JavaScript function would.  

However, when we call this function with the `new` keyword, things change.  First, JavaScript creates a new object, `{}`.  Second, the newly created object is automatically returned from the function.  Note that this occurs even though there is no explicit returns inside of the function.  Not exactly how we remember functions operating.  

Now, as promised, we want our constructor function to provide a mechanism for standardizing the attributes we assign to the object.  We can do this by defining our constructor function with some arguments.

```js
function Puppy(name, age, color, size) {

}

let snoopy = new Puppy('snoopy', 3, 'white', 'medium')
// {}
```

So mission accomplished, sort of.  We see that we can define our constructor function to take in four arguments, and name those arguments appropriately.  However, when we execute the function we are not doing anything with the data that we are passing in, and therefore we are still returning the same blank object.  

To have this object being returned with specific attributes we need to know a couple other things about constructor functions. First, is that when we call a function with the `new` keyword the body of the constructor function is run.  Let's see that:

```js
function Puppy(name, age, color, size) {
  console.log(name)
  console.log(age)
}

let snoopy = new Puppy('snoopy', 3, 'white', 'medium')
// snoopy
// 3
// {}
```

So the name and age is logged, just like our function instructs.  This helps us, because now we can write code such that every time we call our constructor function, we can write code to access the newly created objects and assign some attributes.

Now the only thing we need is a way to access the newly created object, and then assign that newly created objects attributes corresponding to the values passed through.  How do we access that newly created object?  With the `this` keyword.

```js
function Puppy(name, age, color, size) {
  console.log(this)
}

let snoopy = new Puppy('snoopy', 3, 'white', 'medium')
// {}
// {}
```

We'll explore `this` in more detail in a later lesson, but for now know that `this` references the object that receives the method call.  It allows us to reference the object receiving the method from inside a method call.  Here, when we call a function with the `new` keyword, the object receiving the method call is the newly created object.  And so when you see the new object logged twice, the first time is from the `console.log(this)` code, and the second time is because the constructor function returns the newly created object.  So now that we understand that this references the object receiving the method call, or with a constructor function, the newly created object, let's move onto the final step.  

Our final step is to modify that object by assigning it some attributes accordingly.   

```js
function Puppy(name, age, color, size) {
  this.name = name
  this.age = age
  this.color = color
  this.size = size
}

let snoopy = new Puppy('snoopy', 3, 'white', 'medium')
// {name: 'snoopy', age: 3, color: 'white', size: 'medium'}
```
So you can see that we modified our constructor function such that when it is called, it creates the new JavaScript object.  We refer to that JavaScript object from inside of our function with the `this` keyword.  We then assign that new JavaScript object attributes with values that we receive from the arguments passed through.

### It's an easy game from here

The objects that we return operate just like the JavaScript objects you have seen before.  You can read from the object with either the dot or bracket syntax.  

```js
snoopy["age"];
// 3
snoopy.age
// 3
```

And we can modify the objects by assigning new values with dot or bracket syntax:

```js
snoopy["age"] = 4;

snoopy
// {name: 'snoopy', age: 4, color: 'white', size: 'medium'}

snoopy.age = 5

// {name: 'snoopy', age: 5, color: 'white', size: 'medium'}
```

And of course we can create as many objects we want with our constructor function.

```js
function Puppy(name, age, color, size) {
  this.name = name
  this.age = age
  this.color = color
  this.size = size
}

let snoopy = new Puppy('snoopy', 3, 'white', 'medium')
// {name: 'snoopy', age: 3, color: 'white', size: 'medium'}
```

## Summary

We've reviewed working with objects in JavaScript, and started to think about *object-orientated programming* by applying the *constructor function* pattern when creating objects so that we can easily define and reuse objects that we design.

<p class='util--hide'>View <a href='https://learn.co/lessons/js-create-objects-readme'>Creating Objects in JS</a> on Learn.co and start learning to code for free.</p>
