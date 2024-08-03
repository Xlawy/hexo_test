# Code Structure
## Statements & Semicolons

Statements are syntax constructs and commands that perform actions.
Statements can be separated with a semicolon(分号). But in JavaScript, a semicolon may be omitted(省略) in most cases when a line break exists. So the following three pieces of code are equivalent:
```js
// The First One
console.log('Hello'); console.log('World');

// The Second One
console.log('Hello'); 
console.log('World');

// The Third One
// Here, JavaScript interprets the line break as an "implicit" semicolon
// This is called an 'automatic semicolon insertion'
console.log('Hello')
console.log('World')
```
But there are cases when a newline does not mean a semicolon. For example:
```js
console.log(3 + 
1 + 2);
```
The code outputs `6` because JavaScript does not insert semicolons here. It is very intuitively(直观地) obvious that if the line ends with `'+'`, then it will be an 'incomplete expression', so a semicolon there would be incorrect. 
**But there are situations where JavaScript "fails" to assume a semicolon where it is really needed.** So it is best to add a semicolon at the end of each statement even if they are separated by newlines.

## Comments

The comment style in JavaScript is consistent with C++.
- One-line comments start with two forward slash characters `//`.
- Multiline comments start with a forward slash and an asterisk(星号) `/*` and end with an asterisk and a forward slash `*/`.
>[!caution] Nested(嵌套) comments are not supported.
>There may not be `/* .. */` inside another `/* .. */`.
>Such code below will die with an error:
>```js 
>/*
>	/* nested comment */
>*/
>```

# The modern mode, 'use strict'

# Variables

## A variable

To create a variable in JavaScript, use the `let` keyword.
The statement below declares a variable with the name 'massage' and we could put some data into it by using the assignment operator `=`:
```js
let message;
message = 'Hello';
```
We can also declare multiple variables in one line:
```javascript
let user = 'John', age = 25, message = 'Hello';
```
But for the sake of(为了) the readability, please use a single line per variable:
```javascript
let user = 'John';
let age = 25;
let message = 'Hello';
```
>[!info] var and let
>In older scripts, you may also find keyword `var` instead of `let`:
>```js
>var message = 'Hello';
>```
>The `var` keyword is almost the same as `let`. It also declare a variable but in a slightly different way.
>The subtle differences between `var` and `let` will be explained in detail in the subsequent chapter.

## Variable naming

There are two limitations on variable names in JavaScript:
1. The name must contain only letters, digits, or the symbols `$` and `_`.
2. The first character must not be a digit.
When the name contains multiple words, **camelCase** is commonly used.
>[!info] Case matters
>Variables named `apple` and `APPLE` are two different variables.

>[!caution] An assignment(赋值) without 'use strict'
>In old times, it was allowed to create a variable by a mere assignment of the value without using `let`.
>This still works now if we do not put `use strict` in our scripts.
>```js
>num = 5;
>```

## Constants

To declare a constant variable, use `const` instead of `let`.
```js
const myBirthday = '14.01.2005';
```
### Uppercase constants

There is a widespread practice(做法) to use constants as aliases for difficult-to-remember values that are known before the code is execution.
Such constants are usually names using capital letters and underscores.
For instance, we could declare constants for colors in hexadecimal format:
```js
const COLOR_RED = '#F00';
const COLOR_GREEN = '#0F0';
const COLOR_BLUE = '#00F';

let colorOfBG = COLOR_RED;
console.log(colorOfBG); // #F00
```

# Data types

A value in JavaScript is always of a certain type.
There are eight basic data types in JavaScript. We can put any type in variable. For instance, a variable can at one moment be a string and then store a number:
```js
// no error
let msg = 'hello';
msg = 123123;
```
Programming language that allows such things, such as JavaScript, are called **"dynamically typed"**, meaning that there exist data types, but variables are not bound to any of them.

## Number

```js
let n = 123;
n = 12.345;
```
The number type represents both integer and floating point numbers. 
Besides regular numbers, there are three special numeric values belonging to this data type:
- Infinity
- -Infinity
- NaN
```js
console.log(Infinity) // Infinity
console.log(1 / 0) // Infinity
console.log("not a number" / 2) // NaN
```

>[!info] Mathematical operations are safe
>Doing maths is safe in JavaScript. We can do anything, such as divide by zero, treat non-numeric strings as numbers, etc.
>JavaScript will never stop with a fatal error. At worst, we will get `NaN` as the result.

## BigInt

In JavaScript, the number type can safely represent integer values less than $2^{53} - 1$, or more than $-(2 ^ {53} - 1)$. Outside of the safe integer range there will be a precision error, because the number type uses 64-bit storage.
`BitInt` type can represent integers of arbitrary length. A `BigInt` value is created by appending `n` to the end of an integer:
```js
// the 'n' at the end means it is the BigInt;
const bigInt = 114514114514114514114514114514114514114514114514114514114514114514114514114514114514114514114514n;
```

## String

In JavaScript, there are 3 types of quotes:
- Double quotes: `"Hello"`.
- Single quotes: `'Hello'`.
- Backticks: \`Hello\`
Double and single quotes are practically no difference in JavaScript. Backticks are 'extended functionality' quotes. They allow us to embed variables and expressions into a string by wrapping them in `${...}`, for example:
```js
let name = 'John';

console.log(`Hello, ${name}`);
console.log(`the result is ${1 + 2}`);
```
The expression inside `${...}`is evaluated and the result becomes a part of the string. We can put anything in there: such as a variable or an arithmetical expression or something more complex.
## Boolean

The boolean type has only two values: `true` and `false`.
## The 'null' value

In JavaScript, `null` is not a "reference to a non-existing object" or a "null pointer" like in some other languages. It is just a special value which represents "nothing", "empty". It forms a separate type of its own which contains only the `null` value:
```js
let age = null;
```
## The 'undefined' value

The meaning of `undefined` is "value is not assigned". If a variable is declared, but not assigned, then its value is `undefined`:
```js
let age;

console.log(age); // undefined
```
## The typeof operator

The `typeof` operator returns the type of the operand. A call to `typeof x` returns a string with the type name:
```js
console.log(typeof undefined);
console.log(typeof 0);
console.log(typeof 'Zhang');
console.log(typeof 10n); // bigint
console.log(typeof Math); // object
console.log(typeof null); // object
console.log(typeof Symbol('id')); // symbol
```

# Interaction: alert, prompt, confirm

These three functions are used to interact with the user:
`alert`, `prompt` and `confirm`.
## alert

It shows a message and waits for the user to press "OK".
For example:
```js
alert('Hello');
```
The mini-window with the message is call a modal window. The word 'modal' means that the visitor can not interact with the rest of the page, until they have dealt with the window.
## prompt

The function `prompt` accepts two arguments:
```js
result = prompt(title, [default]);
```
It shows a modal window with a text message, an input field for the visitor, and the buttons OK/Cancel.
`title:` The text to show the visitor.
`default:` An optional second parameter, the initial value for the input field.

>[!info] The square brackets in syntax `[...]`
>The square brackets around `default` in the syntax above denote that the parameter is optional, not required.

For instance:
```js
let age = prompt('How old are you?', 100);
alert(`You are ${age} years old!`);
```
## confirm

```js
result = confirm(question);
```
The function `confirm` shows a modal windows with a `quesion` and two buttons: OK and Cancel.
The result is `true` if OK if pressed and `false` otherwise.
For example:

# Type Conversions(转换)

## String Conversion

String conversion happens when we need the string form of a value. We can call the `String(value)` function to convert a value to a string:
```js
let value = true;
value = String(value);
value += '1';
console.log(value); // true1
```
## Numeric Conversion

Numeric conversion in mathematical functions and expressions happens automatically.
For example, when division `/` is applied to non-numbers:
```js
console.log('6' / '2'); // 3
```
We can use the `Number(value)` function to explicitly convert a `value` to a number:
```js
let str = '123';

let num = Number(str);
num +=1;
console.log(num); // 124
```
If the string is not a valid number, the result of such a conversion is `NaN`. For instance:
```js
let age = Number('XinXin is Pig');

console.log(age); // NaN
```
Numeric conversion rules:

| Value              | Convert Result                                                                                       |
| ------------------ | ---------------------------------------------------------------------------------------------------- |
| `undefined`        | `NaN`                                                                                                |
| `null`             | 0                                                                                                    |
| `true` and `false` | `1` and `0`                                                                                          |
| `string`           | Whitespaces from the start and end are removed. If the remaining string if empty, the result is `0`. |
# Basic operators, maths

