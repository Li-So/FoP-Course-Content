Remember the code from *Chapter 2 - Variables & Functions* where you wrote a program that counts upwards? While we managed to make it more efficient by reusing code, it's still a tedious and extremely inefficient way to do it if counting to e.g. 100. Instead, we can use loops that *repeat* code a number of times, depending on conditions we set.

## 5.1 while
The first and "easiest" type of loop is the while loop:
```js
while(true){
	// Do something!
}
```

To enter the loop, the condition inside of the parentheses must be true, executing the code inside. Once the code has been executed, it will loop back, checking the condition once again before looping. Assuming the condition is forever true, the loop will never stop (beware the infinite loop). Each lap of the loop is called an *iteration*.

Let's say we want to count to 10 using a regular while-loop:
```js
let x = 1;

while(x <= 10){
	console.log(x);
	x++;
}
```

Let's walk through it step by step:

1. To avoid having x be re-declared every time the loop runs, we put it outside of the while scope.
2. We assign x the value of 1.
3. The condition is checked. Is x less or equal to 10? 
	-  Not fulfilled? Do steps 4 and 5.
	- Fulfilled? Jump to step 7.
4. The value of x is printed.
5. We increase the value of x by 1.
6. We loop back to step 3.
7. Exit the loop and continue executing code below.

In the example above, we used a condition that won't be true forever (though it could have been if we didn't increment x). This is usually a good thing, since programs shouldn't be trapped in a state where they run forever (where the only chance to escape is by shutting down the running process). 

There are cases wherein we want the program to run for an undecided amount of time, such as in a text-based terminal game, for which the while loop can be appropriate.

If, during the iterations, we want specific actions or conditions to affect the loop, we can use keywords `break` and `continue`. Using `break`, similarly to when using switch statements (see chapter 3), will stop the while loop and exit. The program below illustrates a break , ending the loop when `n === 3`:

```js
let i = 1;

while (i < 5) {
	if (i === 3) {
		console.log("I'm taking a break early. Bye!");
		break;
    }
    console.log("Counting... " + i);
    i++;
}
```

If we instead simply want to skip an iteration, we use `continue`, which will stop statement execution and re-evaluate the condition. By itself, this does not exit the while loop.

```js
let i = 0;

while (i < 5) {
	i++;
	if (i === 3) {
		console.log("I don't feel like counting " + i);
		continue;
    }
    console.log("Counting... " + i);
}
```
## 5.2 do ... while

In certain situations, you may want to perform a minimum of one iteration, with more being optional depending on a condition. In those cases, you can use a do... while loop:
```js
let i = 1;

do {
    if (i === 3) {
        console.log("I don't feel like counting " + i);
        i++;
        continue;
    }
    console.log("Counting... " + i);
    i++;
} while (i < 5);
```

Otherwise, the same principles apply. The possibility remains to be trapped in an infinite loop, you can use `break` to stop early or continue to re-evaluate the condition.
## 5.3 for loop
The for-loop creates a loop with three optional expressions, typically in this format:
```js
for(let i = 0; i < 5; i++){
	// Do something!
}
```

The first of the three expressions is *initialization*. It is some expression or variable declaration that is evaluated only once before the loop begins (usually to declare a new variable for counting). 

The second is the *condition*. If the expression evaluates to true, the statement below is executed. If the expression evaluates to false, execution exits the loop. While it is optional to include an expression, not doing so will make the condition always evaluate to true.

The third is called an *afterthought*, which is an expression evaluated at the end of each loop iteration. This occurs before the next evaluation of the condition and is usually used to update or increment the variable declared in initialization.

Just as we previously declared a while loop in this fashion:
```js
let i = 0;

while(i < 5){
	console.log(i);
	i++;
}
```

We can in a similar (somewhat simpler) manner declare a for loop in this fashion instead, producing the same thing:
```js
for(let i = 0; i < 5; i++){
	console.log(i);
}
```

For loops are best used when you know the exact number of iterations you want to perform, while while loops are used when the number of iterations may be uncertain.

## 5.4 Loop tasks
These tasks won't be particularly challenging and may seem rather random. Most tasks in chapter 6 will require loops to be solved (and make for more interesting tasks), so consider these a warm-up to become more comfortable with just looping. You can make `while` and `for` operate functionally in the same manner, so use what you prefer (but know them both).

### 5.4.1 Counting normally
Make a function that counts from 1 to 50 and prints each number. E.g:
```shell
1
2
3
4
5
...
47
48
49
50
```

Tips:

- Use what you've learned above!

### 5.4.2 Counting... Doubles!
Make a function that counts only even numbers (up to 50). E.g:
```shell
2
4
6
8
10
...
20
22
24
...
46
48
50
```
Tips:

- You can achieve this multiple ways.
	- If statements
	- Changing the iterations (consider substituting i++)
	- Using `continue`

### 5.4.3 Counting backwards
Make a function that counts backwards from 100, but does not print any number between 40 and 60 that is divisible by 2. E.g:

```shell
100
99
98
...
59
57
55
...
41
39
38
37
...
```

Tips:

- Use if and else statements (or switch, if you prefer)
- Using modulus would be appropriate here ( % )
- Keep in mind you should reduce the starting number to count backwards.

### 5.4.4 Exponentiation What-If
Let's imagine for a moment that we cannot use the exponentiation operator (\*\*). Try to implement it on your own using loops!

```js
function calculateExponentiation(a, b){
	// Todo
}
```

Tips:

- I might try to visualize the task as: *a to the power of b, is the same as a multiplied by a, b times...*
	- E.g: 2 ^ 4 = 2 * 2 * 2 * 2 