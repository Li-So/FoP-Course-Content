## 3.1. Booleans and logical expressions
A variable of the type boolean only has the values true and false. Note the code below with some examples using booleans:

```js
let likesDogs = true;
const likesSpiders = false;

let bodyTemp = 39;
let hasFever = (bodyTemp >= 37);
```

Strive to give the boolean variables names that describe what is true or false. If you use any of the comparison operators, the result will be a boolean value (such as the example of `hasFever` above). Using logical operators (`&&` - and, `||` - or, `!` - not), you can combine multiple boolean values:

```js
let isDog = true;
let isCat = true;

let isCanine = isDog && !isCat;
```

It is worth noting that logical expressions are calculated from left to right and that no obviously unnecessary calculations are made. For example:

```js
let isCanine = isDog && !isCat;
```

For `isCanine` to get the value of **true**, `isDog` has to be true and `isCat` has to be false. Assuming `isDog` *isn't true*, we no longer need to check whether the animal *is not* a cat. This is known as a **short-circuit evaluation**.

Similarly, when using the logical operator or, `||`:
```js
let isCanine = isDog || isWolf;
```

Here either `isDog` or `isWolf` need to be true for `isCanine` to be true. Therefore, checking from left to right, if `isDog` *is true* there is no need to calculate `isWolf`.

Test it out with these functions and try to predict what they will print:

```js
function t1(){
	console.log("t1");
	return true;
}


function t2(){
	console.log("t2");
	return true;
}


function f1(){
	console.log("f1");
	return true;
}


function f2(){
	console.log("f2");
	return true;
}


function testBooleans(){
	console.log("Testing booleans!");
	
	let b = t1() && (t2() || f1());
	console.log("Results 1 for b " + b);
	
	b = t1() || t2() || f1();
	console.log("Results 2 for b " + b);
	
	b = f1() || (t2() && (f1() || f2()));
}
```

## 3.2 Boolean coercion
In JavaScript, we don't always have to use explicit booleans for expressions to be evauluated. Several built-in operations that expect booleans first *coerce* their arguments to booleans. These are summarized as follows:

- Booleans are returned as-is
- undefined turns into false
- null turns into false
- 0, -0 and NaN turn into false; other numbers into true
	- Even negative ones!
- 0n turns into false; other BigInts turn into true
- An empty string "" turns into false; other strings turn into true
- Symbols turn into true
- All objects become true.

There are only a handful of values that are coerced into false, called falsy values, while the rest are coerced into true, called truthy values. You can achieve the same effect in JavaScript in two ways:

- Using double NOT `!!x`, negates the value x twice, converting it into a boolean
- The Boolean() function: `Boolean(x)` converts x into a boolean in the same way as above.

## 3.3. if / else statements
The if and else statements allow you to execute code based on conditions. An if statement consists of a boolean expression, written inside of parentheses and some code to be executed *if* the expression results to true. *Else* is used when that statement isn't true.

```js
if(isCanine){
	// Do something only if true!
} else {
	// It wasn't true, do something else!
}
```

Which can of course be expanded into more complex functionality:
```js
let isLoggedIn = true;
let isAdmin = false;

if(isLoggedIn){
	if(isAdmin)
		showAdminDashboard();
	else 
		showUserDashboard();
	
} else {
	showLogin();
}
```

## 3.4 Tasks (if / else)
### 3.4.1 Age Check
Implement a function that takes three boolean arguments:

- Age
- Passport
- ID

Using if-statements, create the function `canLegallyDrink`, which first checks if their age is 18 or above, as well as whether they have either a passport or ID to prove it. 

Experiment with nesting if-else statements, as well as using logical expressions!
```js
function canLegallyDrink(age, hasPassport, hasID) {
	if(age >= 18){
		if(hasPassport || hasID){
			return true;
		}
	} else {
		return false;
	}
}
```

### 3.4.2 A potentially stealthy bug
In the function below, there are is a fairly common error that might be hard to spot. Correct it!

```js
let a = 2 + 2 + 2 + 2;
let b = 4;

function calculateAverage(sum, numbers) {
    if (sum & numbers) {
        console.log("This is: " + sum / numbers);
    } else {
        console.log("I can't calculate this!");
    }
}

calculateAverage(a, b);
```

### **3.4.3 if-else string concatenation**
Let's practice some conditionals. We want to receive some number n, then create a string depending on what it is divisible by. In this case, we'll only check whether it is divisible by 3, 5 or both. If it is divisible by 3, add *"Fizzle "* to the string. If divisible by 5, add the string *"Pop "*. If divisible by both 3 and 5, add only *"FizzlePop "*. 

Tips:

- Use if and if-else statements, they'll be very helpful.
- Consider if there is an operator that could check whether something is divisible by a certain number.

---

## 3.5 switch statements
Let's imagine we have a variable called fruit. It's a string variable containing the name of a fruit, and we want to print something special depending on what type of fruit it is. We could write if statements:
```js
if(fruit === "Papaya"){
	console.log("It is a Papaya!");
} else if(fruit === "Orange"){
	console.log("It is an Orange!");
}
...
```

But this would take a long time and would be quite repetitive. While the repetition in this case might be hard to avoid, we can employ a different method to better match the fruit against a string and print something specific via the *switch statement*.


The switch statement similarly allows code execution based on conditions. It evaluates an expression, matching the value against a series of *case* clauses, and executes statements where the case clause has a matching value, until a break statement is encountered. If there is no match, it will use a default clause. 

This may seem confusing, but observe the example below:
```js
const fruit = "Papaya";

switch (fruit) {
  case "Orange":
    console.log("It is an Orange!");
    break;

  case "Mango":
    console.log("It is a Mango!");
    break;

  case "Papaya":
    console.log("It is a Papaya!");
    break;

  case "Durian":
    console.log("It is Durian!");
    break;

  default:
    console.log("What fruit is that?");
    break;

}
```

Like before, we are trying to match the value of our fruit variable to some fruit name in string format. Here's how it works:

- We input the expression we want to compare, in this case the fruit variable and the value `"Papaya"`.
- The switch statement starts from the first case, `"Orange"` and performs a *strict equality comparison* `===`
- As it returns false, the switch statement keeps proceeding downwards, comparing each case expression (in this case fruit strings) against our fruit variable value.
- Finally, we reach the case `"Papaya"`, which evaluates to true, they are the same. The code below is then executed, printing `"It is a Papaya!"`.
- Since we don't want the switch statement to continue, we use the *break* statement to stop it from comparing further (or alternatively a *return* or *continue* statement).



Assuming we don't stop it using break, execution will proceed to the next case clause, even to the default clause, regardless of whether that clause's expression matches. This is called *fall-through*. Try the example below:

```js
const fruit = "Papaya";

switch (fruit) {
  case "Orange":
    console.log("It is an Orange!");
    break;

  case "Mango":
    console.log("It is a Mango!");
    break;

  case "Papaya":
    console.log("It is a Papaya!");

  case "Durian":
    console.log("It is Durian!");

  default:
    console.log("What fruit is that?");
    break;

}
```

We get three prints, which may not be intended. We can however take advantage of *fall-through* in case multiple conditions are supposed to result in the same code execution:

```js
const animal = "Cow";

switch (animal) {
    case "Cow":
    case "Pig":
    case "Chicken":
    case "Sheep":
        console.log("It is a farm animal!");
        break;
        
    default:
        console.log("Does this animal belong on a farm?");
        break;
}
```

In this case, any of the farm animal cases result in the same console log, while unhandled cases are handled via the default clause. 

It is noteworthy that default does not need to be placed last, and may also trigger a fall-through:

```js
const animal = "Space Cow";

switch (animal) {
	default:
        console.log("Does this animal belong on a farm?");
    case "Cow":
    case "Pig":
    case "Chicken":
    case "Sheep":
        console.log("It is a farm animal!");
        break;
}
```

---

For more complex use, for instance when replacing if...else and with intent to use fall-through, one could also employ a `switch(true)` pattern:

```js
switch (true) {
  case isSquare(shape):
    console.log("This shape is a square.");
	// Fall-through, since a square is a rectangle as well!
  
  case isRectangle(shape):
    console.log("This shape is a rectangle.");
    
  case isQuadrilateral(shape):
    console.log("This shape is a quadrilateral.");
    break;
    
  case isCircle(shape):
    console.log("This shape is a circle.");
    break;
}
```

## 3.6 Tasks (switch)

### 3.6.1 Categories of food
Convert the following function from using if-else to using switch:
```js
function getFoodCategory(food){
	if(food === "Rice"){
		return "Starch";
	} else if(food === "Apple"){
		return "Fruit";
	} else if(food === "Broccoli"){
		return "Vegetable";
	} else if(food === "Chicken"){
		return "Protein";
	} else {
		return "Food category unknown";
	}
}
```

### 3.6.2 switch string concatenation
Remember the if-else string concatenation task using if and if-else statements? Try to reconstruct it using a switch statement instead.
```js
// This is one solution to the issue:
function fizzlePop(n){
	let ans = "";
	switch(true){
		case (n % 5 === 0) && (n % 3 === 0):
			 ans += "FizzlePop ";
		case n % 5:
			ans += "Pop ";
		case n % 3:
			ans += "Fizzle ";
	}
}
```
Tips:

- Using switch(true) may be worth considering.

