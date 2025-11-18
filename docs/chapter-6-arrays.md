The *array* object enables storing a collection of multiple items under a single variable name. For instance, let's say we want to save all the names of the TA's 2025. It wouldn't make much sense to create a new variable for all of them, so we collect them in an array:

```js
const teachingAssistants = ["Bianca", "Evellin", "Oskar", "Liudmyla", "Hannah", "Ronja"];
console.log(teachingAssistants);
```

We deal with array objects much in the same way we deal with any other type of value. The difference, is that we can access each individual value stored inside of the array, giving us the ability to loop through it and do the same thing to every value. We could loop through all the items on an invoice to list them, check for the highest number in a sequence, etc.

The example we used previously contained only strings, but arrays *can contain a mixture of values*...
```js
const numberSequence = [1, 2, 3, 4, 5, 6, 7, 8, 1, 1, 1, 1];
const chaosArray = ["one", 2222, ["wait a minute"], true];
```
...including other arrays! We will address that in more detail later.

To declare an **empty** array (in case we want to fill it later), we write the following:
```js
const numberSequence = [];
```
### 6.1 Indexing and length
While using `console.log()` will print the contents of the array, if we want to use any of those values we will want to access them. To do that, we need to know a few things. 

1. Arrays are *indexed* collections, which means items are numbered. **However**, they *start from zero*. 
	- This means the first item has index 0, the second has index 1 etc. 
	- So, if we for instance want the *third* value of some array, we would use *index 2*.
2. Because they are indexed, we cannot go beyond the length of the array. If the array has a length of 5 (contains 5 values), we cannot access indexes beyond 4, nor indexes before 0, because they do not exist.

Let's first find out how long an array is using the `length` property:

```js
const fruits = ["Apple", "Oranges", "Mango"];
console.log(fruits.length); // 3
```
#### 6.1.1 Accessing values
Now that we know how long the array is, we can attempt to access the elements inside of it using brackets and the index:

```js
const fruits = ["Apple", "Oranges", "Mango"];
console.log(fruits[0]); // "Apple"
```

Keep in mind though, despite `fruits.length` printing a length of 3, we use indexes 0, 1 and 2. Using `fruits[-1]` or `fruits[3]` gives us `undefined`.

#### 6.1.2 Modifying values
Let's assume we want to change a value in the array. To do that, give a single array item a new value:
```js
const fruits = ["Apple", "Oranges", "Mango"];
fruits[0] = "Durian";
console.log(fruits[0]); // "Durian"
```

Be careful though! You are fully able to assign an index far outside the current array length, leaving all the other unassigned indices between undefined:

```js
const fruits = ["Apple", "Oranges", "Mango"];
fruits[10] = "Durian";
console.log(fruits); 
// [ 'Apple', 'Oranges', 'Mango', <7 empty items>, 'Durian' ]
```

You should also note that while unsigned integers (positive whole numbers), are supposed to be used as the indices, you can actually assign using other values in JavaScript. We'll talk about it more in Chapter 7 - Object-Oriented Programming, but for now you just need to **know** that this works, but ought to be avoided:
```js
const fruits = ["Apple", "Oranges", "Mango"];
fruits["froot"] = "Durian";
console.log(fruits["froot"]); 
// "Durian"
```
### 6.2 Array Manipulation
#### 6.2.1 Adding to the array
If you want to add an item or multiple items to the end of the array, you can use `push()`. The push needs to contain the items you want to add into the array. E.g:

```js
const cities = ["Manilla", "Stockholm", "Singapore"];
cities.push("Madrid");
console.log(cities); // ["Seoul", "Stockholm", "Singapore", "Madrid"];
cities.push("Algiers", "Brasília");
console.log(cities); // ["Seoul", "Stockholm", "Singapore", "Madrid", "Algiers", "Brasília"];
```
Using `push()` also returns the new length once the method call is completed, which means you could store it immediately instead of calling using the `length` property right afterwards:

```js
const cities = ["Manilla", "Stockholm", "Singapore"];
const newLength = cities.push("Madrid");
console.log(newLength); // 4
console.log(cities.length); // 4
```

!!! Note
	**`push()` is not the same in p5js. The push method found in p5js to localize drawings and their styles does not exist in regular JavaScript.**	

If you instead want to add to the start of the array, use `unshift()`:
```js
const cities = ["Manilla", "Stockholm", "Singapore"];
cities.unshift("Madrid");
cosole.log(cities)
```
Unshift also returns the length of the new array, similar to `push()`.
#### 6.2.2 Removing from the array
To remove the last item from the array, you can use `pop()`:
```js
const cities = ["Manilla", "Stockholm", "Singapore"];
const removedItem = cities.pop();
console.log(removedItem); // Singapore
console.log(cities.length); // 2
```
Since pop removes the last item, no parameters are required. Using pop does not return the new array length, but instead the item that was removed.

!!! Note
	**`pop()` is not the same in p5js. The push method found in p5js to localize drawings and their styles does not exist in regular JavaScript.**

If you instead want to remove the first item from an array, you can use `shift()`:
```js
const cities = ["Manilla", "Stockholm", "Singapore"];
const removedItem = cities.shift();
console.log(removedItem); // Manilla
console.log(cities.length); // 2
```

#### 6.3 Splicing an array
We can perform even more complex array manipulation via the `splice()` method. Via different parameters, we can remove, replace or add elements in select places (such as the middle). This chapter can be considered part of array manipulation, but more complex (therefore requiring more subchapters).

Splice takes three arguments:

- The starting index (where you want to perform your operation).
	- **Note:** This *CAN* be negative, and will in such cases go backwards (-1 is the last element in the array).
- How many items you want to delete (starting from your starting index)
	- If you omit this parameter, it will delete all elements from your starting index to the end of the array.
- What elements to add to the array.

#### 6.3.1 Element removal:
To remove an element using `splice()`, we specify a starting index and how many to remove. For instance, we may remove only 1 element at index 1:
```js
const cities = ["Manilla", "Stockholm", "Singapore"];
const removedItem = cities.splice(1,1);
console.log(removedItem); // Stockholm
console.log(cities.length); // 2
console.log(cities);
```
 What happened?

- The first 1 in `splice(1,1)` means we target index 1 (`cities[1]` which is Stockholm)
- The second 1 in `splice(1,1)` means we want to remove 1 item.
- Similar to using `pop()`, the `splice()` method returns the removed item or items in a separate array.

Assuming we want to remove multiple elements, such as 2 of them:
```js
const cities = ["Manilla", "Stockholm", "Singapore"];
const removedItems = cities.splice(1,2);
console.log(removedItems); // ["Stockholm", "Singapore"]
console.log(cities.length); // 1
console.log(cities);
```

- We've now removed two elements from the array, starting from index 1.
- Both of the removed elements are returned as their own array.

Let's say we want to remove all elements starting from a certain index in the array. In that case, we don't need to compute how many elements there may be, we simply provide the starting index and the rest are removed:

```js
const numericalSequence = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
const removedItems = numericalSequence.splice(5);
console.log(removedItems); // [6, 7, 8, 9, 10]
console.log(numericalSequence.length); // 5
console.log(numericalSequence); // [1, 2, 3, 4, 5]
```
*Note that 6 is removed, since indexes are counted from 0. It is actually on index 5.*
#### 6.3.2 Element addition:
If we only want to add elements using `splice()`, all we have to do is to target a starting index, use 0 as the amount of elements we want to remove and specify what we want to add. Let's try to add one element using `splice()`
```js
const cities = ["Manilla", "Stockholm", "Singapore"];
const removedItem = cities.splice(1,0, "Seoul");
console.log(removedItem); // []
console.log(cities.length); // 4
console.log(cities); // [ 'Manilla', 'Seoul', 'Stockholm', 'Singapore' ]
```
In this case, we target index 1 (`cities[1]` which has the value Stockholm), we choose to remove 0 items (since we only want to add) and we specify we want to add the value "Seoul" to index 1. 
What happens now?

- The first 1 in `splice(1, 0, "Seoul")` means we target index 1 (`cities[1]` which is Stockholm)
- The 0 in `splice(1,0)` means we want to remove 0 items.
- The string *Seoul* is what we'll be adding to index 1.
- Items already in the array are moved "one step to the right" (they now have a +1 higher index), which means *Seoul* can be placed at index 1 without removing anything.
- The returned `removedItem` is an empty array, since we didn't remove anything.

If we want to add multiple elements, we can add more arguments:

```js
const cities = ["Manilla", "Stockholm", "Singapore"];
const removedItems = cities.splice(1, 0, "Seoul", "Madrid");
console.log(removedItems); // []
console.log(cities.length); // 5
console.log(cities); // [ 'Manilla', 'Seoul', 'Madrid', 'Stockholm', 'Singapore' ]
```

While you can copy the most functionalities of `push()`, `pop()`, `unshift()` and `shift()` (just not returning length), it is more readable to use them when appropriate. 

Just to display the possibility, here's examples of copying each method using splice:
```js
// Copying push()
const cities = ["Manilla", "Stockholm", "Singapore"];
const removedItems = cities.splice(cities.length, 0, "Seoul");
console.log(removedItems); // []
console.log(cities.length); // 4
console.log(cities); // [ 'Manilla', 'Stockholm', 'Seoul' ]
```

```js
// Copying unshift()
const cities = ["Manilla", "Stockholm", "Singapore"];
const removedItems = cities.splice(0, 0, "Seoul");
console.log(removedItems); // []
console.log(cities.length); // 4
console.log(cities); // [ 'Seoul', 'Manilla', 'Stockholm' ]
```

```js
// Copying pop()
const cities = ["Manilla", "Stockholm", "Singapore"];
const removedItems = cities.splice(-1, 1);
console.log(removedItems); // "Singapore"
console.log(cities.length); // 2
console.log(cities); // [ 'Manilla', 'Stockholm' ]
```

```js
// Copying shift()
const cities = ["Manilla", "Stockholm", "Singapore"];
const removedItems = cities.splice(0, 1);
console.log(removedItems); // "Manilla"
console.log(cities.length); // 2
console.log(cities); // [ 'Stockholm', 'Singapore' ]
```


#### 6.3.3 Combining both
In some cases, you want to replace elements and add new ones, which is easily achieved by combining what we've learned so far:
```js
const cities = ["Manilla", "Stockholm", "Singapore"];
const removedItems = cities.splice(1, 2, "Seoul", "Madrid");
console.log(removedItems); // ['Stockholm', 'Singapore']
console.log(cities.length); // 3
console.log(cities); // [ 'Manilla', 'Seoul', 'Madrid' ]
```
Keep in mind, using `splice()` removes items before it adds them.

Another example using a negative starting index:
```js
const cities = ["Manilla", "Stockholm", "Singapore"];
const removedItems = cities.splice(-2, 2, "Seoul", "Madrid");
console.log(removedItems); // ['Stockholm', 'Singapore']
console.log(cities.length); // 3
console.log(cities); // [ 'Manilla', 'Seoul', 'Madrid' ]
```

### 6.4 Tasks (array manipulation)
Since there are more things to cover when using arrays, we'll take a brief intermission to get more comfortable with various methods of array manipulation.
#### 6.4.1 Create an array
Create an array `noodleFlavours` and populate it with the following values:
`"chicken", "beef", "pork", "chili", "vegetables"`. Also create an array `sequenceNumbers` populated with numbers 1 through 10.

We'll be using these arrays to experiment in the later tasks.

#### 6.4.2 Accessing the array
Try different indexes in the array to see what you can access. For instance:
```js
let flavour = noodleFlavours[1];
console.log(flavour) // beef
```

#### 6.4.3 Adding & Removing

- Try adding values `"super chili"` and `"jajangmyeon"` to the `noodleFlavours` array, adding them to the beginning and the end of the array, respectively. 
	- It should look like: `["super chili", "chicken", "beef", "pork", "chili", "vegetables", "jajangmyeon"]`
- Try adding values `5.25` and `5.75` between numbers 5 and 6 in the `sequenceNumbers` array.
	- It should look like: `[1, 2, 3, 4, 5, 5.25, 5.75, 6, 7, 8, 9, 10]`
- Now we'll try to remove the third, fifth and sixth values of `noodleFlavours`, as well as the first and last values of the `sequenceNumbers` array.
	- It should look like: `["super chili", "chicken", "pork", "jajangmyeon"]`
- AND
	- `[2, 3, 4, 5, 5.25, 5.75, 6, 7, 8, 9]`
	
#### 6.4.4 Re-implement push & pop
Since `splice` can be used to add and remove anywhere we want to, you should try to use splice to replicate using push, pop, unshift & shift methods.

### 6.5 Creating copies (spread, from, slice)
Assuming you want to create a copy of an array in JavaScript, there are a number of different methods you can employ. For instance, using direct assignment, using the *spread* and using `slice()`.

```js
const cities = ["Manilla", "Stockholm", "Singapore"];

const citiesCopy1 = cities; // Direct assignment
const citiesCopy2 = [...cities]; // Some array with values
const citiesCopy3 = cities.slice(); // Using slice


console.log(cities);
console.log(citiesCopy1);
console.log(citiesCopy2);
console.log(citiesCopy3);
```



It is noteworthy that most built-in options in JavaScript only create a *shallow copy* of a given array. Defined by MDN:

> A **shallow copy** of an object is a copy whose properties share the same [references](https:// developer.mozilla.org/en-US/docs/Glossary/Object_reference) (point to the same underlying values) as those of the source object from which the copy was made. As a result, when you change either the source or the copy, you may also cause the other object to change too. That behavior contrasts with the behavior of a [deep copy](https:// developer.mozilla.org/en-US/docs/Glossary/Deep_copy), in which the source and copy are completely independent.

Let's walk through an example.
```js
const cities = ["Manilla", "Stockholm", "Singapore"];
const citiesCopy = cities;

citiesCopy[0] = "London";
console.log(citiesCopy[0]); // London
console.log(cities[0]); // London

citiesCopy.push("Tokyo");
console.log(citiesCopy[3]); // Tokyo
console.log(cities[3]); // Tokyo

citiesCopy.splice(1,0, "Brasília");
console.log(citiesCopy[1]); // Brasília
console.log(cities[1]); // Brasília
```

- We have an array cities that we want to copy and change.
- We change the first value in `citiesCopy` at index 0...
- ...but `cities[0]` changed too!
- Despite trying to use
	- assignment
	- push
	- splice

To avoid this and ensure completely separate copies, we would need to create a *deep copy*. There are no built-in ways to create them in JavaScript, but it is possible via a workaround (we'll talk about it later though).

!!! Note
	The slice method and the spread operator will create a "one level" deep copy, meaning it works for things that are not multi-dimensional.

### 6.6 Looping
Arrays are most likely what you will find most use for looping over, using the index across iterations. This is the simplest example, using a while-loop:

```js
const cities = ["Manilla", "Stockholm", "Singapore"];
let i = 0;

while(i < cities.length){
	console.log(cities[i]);
	i++;
}
```

The condition and iterations should reasonably ensure that the index does not attempt to access a value outside of the array's length (e.g -1 or in this example, 3). Also make a note of ensuring no infinite loops!

Here's also an example using the for-loop:
```js
const cities = ["Manilla", "Stockholm", "Singapore"];

for(let i = 0; i < cities.length; i++){
	console.log(cities[i]);
}
```

#### 6.6.1 For ... of
For some, a more convenient and readable route is using `for ... of`. In cases where indices are not required, we could instead loop over the same `cities` array like this:
```js
const cities = ["Manilla", "Stockholm", "Singapore"];

for (const city of cities){
	console.log(city);
}
```

### 6.7 Strings & arrays
Now that we're comfortable enough with both arrays and looping, it is worth noting that strings can be handled similarly to arrays. Using an index in a string will return the character in that position:

```js
const city = "Singapore";
const letter = city[0];
console.log(letter);
```

The character value stored at that index cannot be changed as strings are immutable, but a copy with a modification can be achieved with a string method, e.g. `replace()`:

```js
const city = "Singapore";
let newCity = city.replace("S", "Z");
console.log(newCity); // "Zingapore"
```


### 6.8 Multidimensional arrays 
Working with arrays can quickly become complicated to visualize as you nest arrays inside of arrays. It is still feasible to visualize with perhaps one or two nested arrays (creating 2D and 3D arrays respectively), but beyond that becomes quite difficult.

Let's say we were making tic-tac-toe (aka three-in-a-row). We could create multiple arrays, for each row (or column if you prefer), but then you would need to loop across several arrays to check for a winner, which is annoying and inefficient.

Instead, imagine the following; you are going to draw a 3 x 3 tic-tac-toe board. To do that, you do the following:

1. You draw the first box to the top left.
2. You then continue to draw boxes below it, making the first column.
3. You draw a box to the right of the top box.
4. You draw the boxes below that box.
5. You once again, draw a box to the right of the top box.
6. You draw boxes below that box.

Here are some diagrams for visualization (**NOT CODE, JUST PSEUDOCODE**):

1. 
```
[]
```

2. 
```
[]
[]
[]
```
3. 
```
[] []
[]
[]
```
4. 
```
[] []
[] []
[] []
```
5. 
```
[] [] []
[] []
[] []
```
6. 
```
[] [] []
[] [] []
[] [] []
```

What we have now done is effectively instructions on how to draw a 3 x 3 tic-tac-toe board. This is incidentally also how creating a 2D array roughly works. We specify how many columns we want (how many of the top-boxes will we draw?) and then we figure out how many rows we want (how many boxes do we draw below?).

The value of the array is therefore another, nested, array containing 3 values for tic-tac-toe board positions. To access those values, you will need to use multiple indexes:

```js
let ticTacToeBoard = [[1,2,3], [4,5,6], [7,8,9]];
let firstSpace = ticTacToeBoard[0][0]; // 1
let fifthSpace = ticTacToeBoard[1][1]; // 5
```

Which can be visualized as:

```
[ 1 ]  [ 2 ]  [ 3 ]
[ 4 ]  [ 5 ]  [ 6 ]
[ 7 ]  [ 8 ]  [ 9 ]
```

OR

```
[ 1 ]  [ 4 ]  [ 7 ]
[ 2 ]  [ 5 ]  [ 8 ]
[ 3 ]  [ 6 ]  [ 9 ]
```
### 6.9 Tasks (arrays & strings)

#### 6.9.1 Accessing a 2D array
Create the following array `let ticTacToeBoard = [[1,2,3], [4,5,6], [7,8,9]];` and try to access the values *3, 7 and 9*. `console.log` them! 

#### 6.9.2 Finding the largest number
Loop over the following array `[1,124,321,352,3246,6,436,64,436]` to try to locate the largest number. 

Tips:

- Keep track of the largest number you've found so far with a variable.
- Using an if-statement, replace the number you've stored in a variable with the one you've found.
- Try it on different types of arrays:
	- `[18,2,124,124,2531,254,63]`
	- `[1248,2345,675,796,546,79]`
	- `[423,5231,756,678,7809]`

#### 6.9.3 Email validity
Let's do a very simple email validity check. If there is no `@` sign, it is probably invalid. If there are two or more, it is equally invalid. Build a function that checks an array of emails, e.g. `["valid@valid.com", "invalid.invalid.com", "valid@invalid@valid.com"]` and returns `false` if any of them are not valid. 

The example array given should return `false`.

Tips:

- Using the string method `includes()` might be a good fit. Look it up on MDN!
- Use an if statement with includes to see whether something works or not.