User# Creating Objects

## Objectives
+ Create a constructor function
+ Use a constructor function to create an object
+ Explain what a constructor function is and how it works
+ Explain what `this` is in the context of an object

## Introduction

So far we have mainly examined primitive data types like strings and integers.  As you have seen, it sometimes becomes convenient to represent data with objects, which gives us key value pairs. For example, we may represent a user as the following:

```javascript
  let bobby = {name: 'bobby', age: 20, hometown: 'Philadelphia'}

  // our JavaScript object
````

Now imagine that we had a couple of users:

```js
let bobby = {
  name: 'bobby',
  age: 20,
  hometown: 'Philadelphia'
}

let susan = {
  name: 'susan',
  age: 28,
  hometown: 'Boston'
}

```

Great. Two nice users.

Note, that with a both objects sharing exactly the same keys, and only the values differing, we are *[repeating ourselves](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself)*.  We would like a mechanism to construct objects with the same attributes (that is, keys), while assigning different values to those keys.   

### Constructor Function

Instead of typing out each attribute separately with the literal syntax, we can use a *constructor function*.  It operates as a factory for new objects.

Let's write a constructor function that returns a Javascript object without any attributes:

```js
function User() {

}

User()
// undefined


new User
// {}
```

Let's unpack the code above.  First, we declare a function called `User`.  We capitalize the name of the function simply as a convention, to indicate that we will be using this function differently.  This function is just a plain old JavaScript function.  We demonstrate that by calling `User()` and seeing that it returns undefined, just like any other blank JavaScript function would.  

However, when we call this function with the `new` keyword, things change.  First, JavaScript creates a new object, `{}`.  Second, the newly created object is automatically returned from the function.  Note that this occurs even though there is no explicit returns inside of the function.  Not exactly how we remember functions operating.  

Now, as promised, we want our constructor function to provide a mechanism for standardizing the attributes we assign to the object.  We can do this by defining our constructor function with some arguments.

```js
function User(name, age, hometown) {

}

let bobby = new User('bobby', 20, 'Philadelphia')
// {}
```

So mission accomplished, sort of.  We see that we can define our constructor function to take in four arguments, and name those arguments appropriately.  However, when we execute the function we are not doing anything with the data that we are passing in, and therefore we are still returning the same blank object.  

To have this object being returned with specific attributes we need to know a couple other things about constructor functions. First, is that when we call a function with the `new` keyword the body of the constructor function is run.  Let's see that:

```js
function User(name, age, hometown) {
  console.log(name)
  console.log(age)
}

let bobby = new User('bobby', 20, 'Philadelphia')
// bobby
// 20
// {}
```

So the name and age is logged, just like our function instructs.  This helps us, because now we can write code such that every time we call our constructor function, we can write code to access the newly created objects and assign some attributes.

Now the only thing we need is a way to access the newly created object, and then assign that newly created objects attributes corresponding to the values passed through.  How do we access that newly created object?  With the `this` keyword.

```js
function User(name, age, hometown) {
  console.log(this)
}

let bobby = new User('bobby', 20, 'Philadelphia')
// {}
// {}
```

We'll explore `this` in more detail in a later lesson, but for now know that `this` references the object that receives the method call.  It allows us to reference the object receiving the method from inside a method call.  Here, when we call a function with the `new` keyword, the object receiving the method call is the newly created object.  And so when you see the new object logged twice, the first time is from the `console.log(this)` code, and the second time is because the constructor function returns the newly created object.  So now that we understand that this references the object receiving the method call, or with a constructor function, the newly created object, let's move onto the final step.  

Our final step is to modify that object by assigning it some attributes accordingly.   

```js
function User(name, age, hometown) {
  this.name = name
  this.age = age
  this.hometown = hometown
}

let bobby = new User('bobby', 20, 'Philadelphia')
// {name: 'bobby', age: 20, hometown: 'Philadelphia'}
```
So you can see that we modified our constructor function such that when it is called, it creates the new JavaScript object.  We refer to that JavaScript object from inside of our function with the `this` keyword.  We then assign that new JavaScript object attributes with values that we receive from the arguments passed through.

### It's an easy game from here

The objects that we return operate just like the JavaScript objects you have seen before.  You can read from the object with either the dot or bracket syntax.  

```js
bobby["age"];
// 20
bobby.age
// 20
```

And we can modify the objects by assigning new values with dot or bracket syntax:

```js
bobby["age"] = 4;

bobby
// {name: 'bobby', age: 4, hometown: 'Philadelphia'}

bobby.age = 5

// {name: 'bobby', age: 5, hometown: 'Philadelphia'}
```

And of course we can create as many objects we want with our constructor function.

```js
function User(name, age, hometown) {
  this.name = name
  this.age = age
  this.hometown = hometown
}

let bobby = new User('bobby', 20, 'Philadelphia')
// {name: 'bobby', age: 20, hometown: 'Philadelphia'}

let fidoDido = new User('sally', 28, 'Boston')
// {name: 'sally', age: 28, hometown: 'Boston'}
```

## Summary

We've reviewed working with objects in JavaScript, and started to think about *object-orientated programming* by applying the *constructor function* pattern when creating objects so that we can easily define and reuse objects that we design.

<p class='util--hide'>View <a href='https://learn.co/lessons/js-create-objects-readme'>Creating Objects in JS</a> on Learn.co and start learning to code for free.</p>
