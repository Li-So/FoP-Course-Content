This chapter will mainly focus on getting used to variables and functions. Using only values and variables does not make for very interesting tasks, therefore we will include functions in the same chapter.

So far, you've used `console.log()` to print things from your program without an explanation of what it really is. It is a function built into JavaScript that we can call on to print things, but now it is time we build our own functions.

## 2.1 Basic functions
### 2.1.1 Count to Three
Create a function using `console.log()` to print 1, 2, 3 each on separate lines. 
```js
function countToThree(){
	// TODO
}
```

Once you're done, save and run the code... nothing will happen. Because to run the code, you need to *call* the function:

```js
function countToThree(){
	// TODO
}

countToThree();
```

Now you should see 1, 2, 3 (on separate lines) in your terminal!
### 2.1.2 Count to Four
Now let's assume we want to create a program that writes 1, 2, 3, 4 instead. We could write the same function `countToThree()` again, add a fourth log and rename it `countToFour()`. That would be inefficient though, as we've already done a majority of the work in `countToThree()`. Therefore we will reuse it.

```js
function countToFour(){
	// TODO
}
```

Change the code above so that it counts all the way to four by doing the following:

- Add a function call to `countToThree()` from `countToFour()`.
- Make `countToFour()` print a 4 after the call to `countToThree()`.
- Call the `countToFour()` function!

## 2.2 Variables in functions
### 2.2.1 The Pythagorean Theorem

Don't worry, we won't deep dive into mathematics in this course, but it makes for a good example in this case. According to the Pythagorean theorem, in a right triangle, the square of the length of the hypotenuse is equal to the sum of the squares on the lengths of the other two sides. This can be expressed via the formula:

$a^2+b^2=c^2$

We will be using it to determine the length of the hypotenuse in a given triangle:

${\sqrt {a^2 + b^2}} = {\sqrt {c^2}}$

Below is one way to write the function for a triangle with the side lengths 3 and 4.

```js
function calculateHypotenuse() {
  let a = 3;
  let b = 4;
  
  let aSquared = a * a;
  let bSquared = b * b;
  
  let cSquared = aSquared + bSquared;
  let c = Math.sqrt(cSquared);

  console.log("a is " + a + " and b is " + b);
  console.log("The sum of the squared variables is " + cSquared);

  console.log("The hypotenuse therefore has the length of: " + c);

}
```

Explanation:
- The function introduces the first variables `a` and `b`, initiating them with values 3 and 4.
- We then create new variables for the squared values of a and b with appropriate naming, such as `aSquared` containing the value 9.
- Towards the end, we calculate c via `Math.sqrt()`, providing us with the square root of `cSquared`. 
	- `Math.sqrt()` is another function provided by JavaScript.
	- We could just as easily have used the power of operator to replace `Math.sqrt()` in this case.
- Finally, the `console.log()` mixes strings and numbers to present us with the result.
- Try calling the function!


### 2.2.2 Using parameters and arguments

In the previous implementation of `calculateHypotenuse()`, we always calculate the same triangle. Therefore, we will change the current to use parameters, allowing the caller to provide us the values for a and b. Let's also get rid of some unnecessary variables.

```js
function calculateHypotenuse(a, b) {
  let cSquared = a*a + b*b;
  let c = Math.sqrt(cSquared);

  console.log("a is " + a + " and b is " + b);
  console.log("The sum of the squared variables is " + cSquared);
  console.log("The hypotenuse therefore has the length of: " + c);
}
```

Since we have modified the function to now include function parameters, we can call the function like this:

```js
calculateHypotenuse(1, 2);

const x = 1;
const y = 2;
calculateHypotenuse(x, y);

const a = 2;
const b = 3;
calculateHypotenuse(b, a); 
// Notice how we switched? if not, look at the function above

```

Make sure to study the printed text to make sure you understand what happens. 

Some things to make special note of:
- The first function call uses `a = 1` and `b = 2`.
- The second function call uses the values of variables x and y
	- once again calling the function with `a = 1` and `b = 2`
- The third function call uses values of variables a and b
	- *calling the function with a = 3 and b = 2*
	- The reason being that the variables declared outside of the function are **completely separate** from the variables declared outside. Variables only exist in their local scope where they are declared.



### 2.2.3 Returning a value
In the next version of this function, we will add `return c;` to the very bottom. This will enable us to use the value calculated by the function to do something else later:

```js
function calculateHypotenuse(a, b) {
  let cSquared = a*a + b*b;
  let c = Math.sqrt(cSquared);

  console.log("a is " + a + " and b is " + b);
  console.log("The sum of the squared variables is " + cSquared);
  console.log("The hypotenuse therefore has the length of: " + c);
  
  return c;
}


let length = hypotenuseLength(1, 2);
console.log("The length of the hypotenuse is " + length);
```

By using return c, we can now access the value outside of the function.


### 2.2.4 Making the function clean
```js
function calculateHypotenuse(a, b) {
  let cSquared = a*a + b*b;
  let c = Math.sqrt(cSquared);  
  return c;
}


let length = hypotenuseLength(1, 2);
console.log("The length of the hypotenuse is " + length);
```

When programming, you should try to aim for clean functions. In those cases, it is easier to test them and to reuse them (e.g. have the function give you the value and to print it separately). Keep in mind, functions should also be as easy to read as possible. 

Below is an alternative implementation of `calculateHypotenuse(a, b)` using the standard function syntax:

```js
function calculateHypotenuse(a, b) {  
  return Math.sqrt(a*a + b*b);
}
```

Another variant using an arrow function:

```js
calculateHypotenuse = (a, b) => Math.sqrt(a*a + b*b);
```

##  2.3 Tasks (functions & variables)

### 2.3.1 Program printFullName
Make a simple program that takes two parameters: `firstName` and `lastName`. Return the person's full name so that it prints like this:
```js
let fullName = printFullName("Linus","Sonnerhed");
console.log(fullName);
// Prints: Linus Sonnerhed
```

### 2.3.2 Improve the function
This function isn't very clean, nor could we reuse it if the variables were different. Re-write or *refactor* the function to improve it.
```js
function calculateSleep(){
	var lightSleepHours = 5;
	var deepSleepHours = 2;
	console.log(lightSleepHours + deepSleepHours);
}
```
### 2.3.3 Program turn-order
Let's assume there are a number of people playing something similar to UNO, where you can force other players to skip their turns. If this variant of UNO allowed multiple skips, it may be hard to know whose turn it really is.

Since each player has a turn order they start with, we can use numbers to represent them (1,2,3) and use that as input for a function, as well as whose turn it is before the skips and how many skips there are:

```js
function getTurnOrder(totalPlayers, currentTurn, skipAmount){
	// TODO
}
```

Given the total amount of players, whose current turn it is (player 1, 2 or 3 etc.) and how many turns we want to skip, return whose turn it is supposed to be, e.g:
```js
let currentTurn = getTurnOrder(3, 1, 5);
console.log(currentTurn); // Prints 3, now we know it is player 3's turn!
```

Tips:

- There may be a use for the *modulus operator* (`%`) in this case...

### 2.3.4 Program calculateBookCost
Sometimes buying books for hundreds of SEK may feel expensive (especially as a computer science student for which much material can be found for free). As a coping mechanism, one may consider calculating the cost per hour of reading, to make it more bearable.

Below, write a function that calculates the cost of a book over a certain amount of time. Have the function include parameters for:
- How much the book will cost?
- How many pages the book has?
- How many percent of the book do you intend to read?
- How many minutes does it take to read and understand a page?

Finally, have the function print the final calculation. 

Example print:
```
You're expected to dedicate ca 82.1 hours to this book.
The book is therefore calculated to cost you 6.25 SEK/h.
```
(print above is based on: cost being 513 SEK, 657 pages, reading 50% of them, 15 minutes to understand a page)

Some tips:

- Add some parameters with easily understood names, e.g. `bookCost`, `pageCount`, `readPercent`, `comprehensionTime` (in minutes)
- Add a variable `totalHours` and initiate it with the correct value on the same line.
- Print the cost of the book per hour!
	- If you want to make it look prettier, use `.toFixed(2)` on a variable to set a two decimal accuracy, e.g. `bookCost.toFixed(2)`


### 2.3.5 Change Calculation
Let's assume you're working at a coffeeshop and need a quick way to calculate change. There are coins and bills of these values: 500, 200, 100, 20, 10, 5, 2, 1. If you call the function which you are about to create, `printChange(947)`, it should print the following:

```bash
947 is:
1 x 500
2 x 200
0 x 100
2 x 20
0 x 10
1 x 5
1 x 2
0 x 1
```

This task will not require a clean function.

```js
function printChange(totalPrice){
	// TODO
}
```
Tips:

- Try to keep the calculation simple without too much math. Here's a suggestion for the first three lines of the program:
```js
let remainingChange = totalPrice;
let number500s = Math.floor(remainingChange / 500);
remainingChange -= number500s * 500;
```

- `Math.floor()` is useful for achieving division via whole numbers (integer division).
	- This is not necessary in some languages, as integers and floats are wholly separate data types.