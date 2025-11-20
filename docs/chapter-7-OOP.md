Objects in JavaScript are collections of related data and/or functionality. Usually they contain several variables and functions, referred to as **properties** and **methods** when inside objects. They will combine everything you've learned so far about JavaScript and will be used to structure your game later on!

## 6.1 Object basics
### 6.1.1 Declaring an object
Let's look at a basic and empty object called dog:

```js
const dog = {};
```

To declare a new object, we use curly braces in a fashion similar to what we've used previously with variables. The object we have above does not have any **properties** or **methods**, so we'll add some below:

```js
const dog = {
	name: "Khloe",
	age: 3,
	bark: function(){
		console.log("Bark!");
	}
}
```
What did we just write?

- We've now added two properties: `name` and `age`, as well as a function called `bark()`. 
- We may observe that, similarly to variables, we declare some data name and some data value, separated by a colon. 
- Both **properties** `name` and `age` have primitive data types (a string and a number respectively), though it could be Booleans or arrays or other objects as well.
- The **method** `bark()` can contain anything we might put in a normal function, though for now we'll keep it simple and only have it print `Bark!`
	- You can alternatively write `bark(){ console.log("Bark!")` instead of using `bark: function(){ console.log("Bark!")}`.

!!! Note
	When creating objects in this fashion, separate the values of each row with commas or you'll encounter an error.

If you want it in a more generic format, you may consider the following:

```js
const someObject = {
	member1Name: member1Value,
	member2Name: member2Value,
	member3Name: member3Value,
}
```

Of course, objects can also contain smaller objects. If we had a person object, like this:

```js
const person = {
	name: ["Linus", "Sonnerhed"],
}
```

We could also change it to:

```js
const person = {
	name: {
		first: "Linus",
		last: "Sonnerhed",
	},
}
```

This provides further structuring in more complex objects and enables us to give further context for nested object data. Both `first` and `last` are part of the smaller object `name`, giving us as programmers context for what they really mean without having to extend the data name.

What we've created is called an **object literal**. In essence, we've written out the object contents as we've come to create it, which is different to instantiating them from **classes** (more on that later). The reason we use objects frequently is often due to structure and data transfer. When you have related data in this fashion, it would be less efficient to send as several individual items. Arrays may be preferable in certain situations, but objects are usually the standard.

### 6.1.2 Accessing an object
Let's now try to access some of these properties and call the method.There are two different ways to do this, using either the **dot** notation or the **bracket** notation. In both cases, we will need to access the **namespace** of an object to access anything inside of the object. For instance, we cannot simply call `bark()` in our code and expect it to know we mean the method we declared in the dog object. 

Let's look at the dot notation first (using the dog object from previously):

```js
dog.name; // Khloe
dog.age; // 3
dog.bark(); // Bark!

// Access the namespace by using dog and use dot to access the contents.
```

Let us also compare this against brackets (using the dog object from previously):

```js
dog["name"]; // Khloe
dog["age"]; // 3
dog["bark"](); // Bark!

// Access the namespace by using dog and use brackets and the property OR method name as strings. Functions require the parentheses for arguments after the name.
```

Both methods also work for nested objects (using the person object from previously):

```js
person.name.first // Linus
person.name.last // Sonnerhed

person["name"]["first"] // Linus
person["name"]["last"] // Sonnerhed
```

One may find that using brackets is quite similar to accessing arrays, which is why objects are sometimes called **associative arrays**, as you map strings to values instead of indexes to values. Dot notation is generally preferred for readability, but there are cases where brackets are the only option (explained later in this chapter).

### 6.1.3 Changing an object

While retrieving (or *getting*) object members is useful, we also want to update or *set* them. You can do this with both dot and bracket notation:

```js
dog.age = 4;
person["name"]["last"] = "Cayna"
```

However, we are not constrained to only updating existing object members. We can also set brand new ones!

```js
dog.mood = "Happy";
person["Hobbies"] = ["Fishing", "Skiing"];
person.shout = function(){
	console.log("HEY!");
}
```

In cases where we want to dynamically get or set object members, we can use brackets. For instance, if we wanted a function that printed a method's properties:

```js
const person = {
  name: "Linus",
}

function logProperty(propertyName){
  console.log(person[propertyName]);
}

logProperty("name"); // "Linus"
```

In this scenario, we want to receive a string argument which the function will use to print an object property. This would not be possible using dot notation.

In a different scenario, assuming we want to set both the member name and value dynamically, we can also use brackets. Let's assume we have a website where we use the `person` object for every user. Assuming the user wants to fill in their own details, they can add properties and methods as they choose: 

```js
const dataName = "height"
const dataValue = "3.33m";

person[dataName] = dataValue;
```

Without having provided a standard value for height beforehand, we can now set it dynamically should the user want to.

### 6.1.4 The *this* keyword
When working with objects, you may want to use object properties or methods in other parts of the object. For instance, let's enable a user to introduce themselves:

```js
const person = {
	name: {
		first: "Linus",
		last: "Sonnerhed",
	},
	introduceSelf(){
		console.log(`Hello, my name is ${this.name}.`)
	}
}
```

Using this, we can refer to the property `name` inside of the person object to create a method using that same property. If we had two separate object literals:

```js
const person1 = {
  name: "Linus",
  introduceSelf(){
    console.log(`My name is ${this.name}`);
  }
}
```

```js
const person2 = {
  name: "Dennis",
  introduceSelf(){
    console.log(`My name is ${this.name}`);
  }
}
```

They would print their own names, as this only refers to the current object the code is being executed in.

## 6.2 Making many objects
While object literals are useful, it would be too inefficient to write them in larger quantities. Instead, we can make a blueprint or rough "shape" of an object, including what properties and methods it should have. Once we have them, we can update the values of the objects that are different.

### 6.2.1 Function to make objects

For now, we'll create a basic object creating function:

```js
function createPerson(name){
	const obj = {};
	obj.name = name;
	obj.introduceSelf = function(){
		console.log(`Hi, I'm ${this.name}`);
	}

	return obj;
}
```

What does it do?

- It creates a new and empty object
- It initializes a name property with the value name (from the function parameters)
- It initializes an introduceSelf method which uses the name property value
- It finally returns the object.

This method works and could be used to create multiple people:

```js
const linus = createPerson("Linus");
linus.introduceSelf(); // Hi! I'm Linus.

const pratt = createPerson("Pratt");
pratt.introduceSelf(); // Hi! I'm Pratt.
```

Now all of our objects will be created in the same manner which is a very common pattern. 

### 6.2.2 Constructors

Our approach is somewhat inefficient however, as we have to create an empty object, initialize it, return it... Things that would be the same for creating any object generating function. 

The more efficient route is to use a **constructor**, which functions very similarly to our previous function. The difference, is that a constructor will:

- Create a new object
- Bind *this* to the object so you can use it in the constructor code
- Run the code in the constructor
- Return the new object

In essence, removing the parts of our previous function that were unnecessarily repetitive. By convention, constructors always start with a capital letter and are named for the type of object they create. 

Let's convert our old function into a constructor:

```js
function Person(name) { 
  this.name = name;
  this.introduceSelf = function(){
    console.log(`Hi! I'm ${this.name}`);
  };
}
```

We no longer need to create an explicitly create an object and return it, as it is handled by the constructor. We rename the function `Person` as that is what it creates and capitalized for convention.

When creating new objects, the only difference from before is that we use the **new** keyword for new objects:

```js
const linus = new Person("Linus");
linus.introduceSelf(); // Hi! I'm Linus.

const dennis = new Person("Dennis");
dennis.introduceSelf(); // Hi! I'm Dennis.
```

## 6.3 Previous familiarity
These examples are probably familiar, as you've already been interacting with objects throughout the course. They are more complex than the objects we've created, but they are objects nonetheless.

Some examples include:

- The console object, providing you with e.g:
	- `console.log()`
	- `console.table()`
- The math object, providing you with e.g:
	- `Math.abs()`
	- `Math.floor()`
- The array object, providing you with e.g:
	- `.push()`
	- `.pop()`


## 6.4 Object-Oriented Programming