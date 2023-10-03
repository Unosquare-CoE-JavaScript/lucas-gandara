# You dont know js yet

## Chapter 2: Surveying Js.
**The best way to learn Js is by writint Js**

Regardless of which code organization pattern (and loadingmechanism) is used for a file (standalone or module), youshould still think of each file as its own (mini) program, whichmay then cooperate with other (mini) programs to performthe functions of your overall application.

### Values:
Along as variables, though we can have just the values, is very common to save them into containers called _variables_. To declare a variable there are three options _var_, _let_ and _const_. The main difference is that let and const declares a variable to be used in that part ofthe program, and optionally allows initial value assignment, this is called _block scoping_.

```js
var adult = true;
if (adult) {
    var name = "Kyle";
    let age = 39;
    console.log("Shhh, this is a secret!");
}

console.log(name);
// Kyle

console.log(age);
// Error!
```

The attempt to access age outside of the if statement resultsin an error, because age was block-scoped to the if, whereasname was not. Also, if you declare a variable with _const_ the Js engine won't let you reasign this variable to another value.

#### Primitives: 

Values are data. In Js we can have two tipes of values, primitives and objects. String literals are strings are ordered collections of characters,usually used to represent words and sentences.
Consider you have a variable name _firstName_ with value 'Lucas':

```js 
const firstName = 'Lucas'

console.log("My first name is: ${firstName}");
// My first name is: ${firstName}

console.log("My first name is: ${firstName}");
// My first name is: ${firstName}

console.log(`My first name is: ${firstName}``);
// My first name is: Lucas
```
    
when using backtips(`) we can resolve variables whithin the string literas. This is called [**String Interpolation**](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals).

Wether to use ' or " is up to you, just pick one and sitck to it in your entire application and use ` when you need string interpolation.

Other primitives types could be numbers or booleans:
```js
const age = 25; // Could be naturals numbers
const average = 2.555; // Could be decimals

const isSoftwareUpdated = false; // Booleans could be either True or false
const isGreaterThan = true;
```

Other primitives in Js are _null_ and _undefined_. While there are differences between them (some historic andsome contemporary), for the most part both values serve thepurpose of indicating emptiness (or absence) of a value. It's safer and and best option to use undefined.

The las primitive in Js is _symbol_ that are mostly used to create private attributes.

#### Arrays and Objects:
Arrays are a special type of object that’scomprised of an ordered and numerically indexed list of data:

```js
const names = [ 'Lucas', 12, False ];

// They have atributes such as:
names.length;
// 3

// You can index them:
names[0];
// Lucas
```

Remember htat Array can hold any type of data.

Objects are more general: an unordered, keyed collection ofany various values.

```js
const person = {
    name: 'Lucas',
    age: 26,
    isMarried: false,
    skills: ['Js', 'React']
}
console.log(person.age);
// 26

console.log(person['age']);
// 26
```

Tip from the book:

    If you stick to using const only with primitivevalues, you avoid any confusion of re-assignment(not allowed) vs. mutation (allowed)! That’s thesafest and best way to use const.

#### Functions:
Functions are procedures, a collection of statements that can be invoked one or several times. They can be declared in many ways, like a definition:

```js
function add(number1, number2) {
    return number1 + number2;
}
```
Or like an asigment:

```js
const add = function (number1, number2) {
    return number1 + number2;
}
```

It's important that, since functions are special types of objects and can be assigned to variables, they can be passed around as parameters to other functions. The are treated as values by the Js engine.

#### Comparisons in Js, Equal...ish
Comparison may be tricky for new users, in Js there are several ways to **Compare** two values _==_, _===_, Object.is(...), but when to use each of them?

You may be tempted to think to use _===_ in all cases, however, JS does not define _===_ as structural equality for object values.Instead, _===_ uses identity equality for object values. Since in Js all objects are held by reference, are assigned and passed byreference-copy, and are comparedby reference (identity) equality. Consider:

 ```js
var x = [ 1, 2, 3 ];
// assignment is by reference-copy, so
// y references the *same* array as x,
// not another copy of it.
var y = x;
y === x;           // true
y === [ 1, 2, 3 ]; // false
x === [ 1, 2, 3 ]; // false
 ```

_==_ on the other hand is knonw as the coercive equality, this means that when used, _==_ operator will try to convert both sides to be the same types and then _==_ operator does the same thing as _===_. So when the same types are being compared, _===_ and _==_ **Do the exact same thing!**

### Classes
A class in a program is a definition of a “type” of customdata structure that includes both data and behaviors thatoperate on that data. Classes don't ocupy memory themselves but they are blueprints to create your own types.

## Es Modules:
They were introduced in the language in ES6. The wrapping context is a file. ESMs are always file-based, one file, one module. You just import it to use an instance of a module, so an ECMA Script Module is in fact a [singleton](https://refactoring.guru/es/design-patterns/singleton).

