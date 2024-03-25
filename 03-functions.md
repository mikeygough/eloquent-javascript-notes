A function definition is a regular binding where the value of the binding is a function. For example, this code defines square to refer to a function that produces the square of a given number:

```javascript
const square = function (x) {
  return x * x;
};

console.log(square(12));
// → 144
```

There is a slightly shorter way to create a function binding. When the function keyword is used at the start of a statement, it works differently:

```javascript
function square(x) {
return x \* x;
}
```

This is a function declaration.
There is one subtlety with this form of function definition.

```javascript
console.log('The future says:', future());

function future() {
  return "You'll never have flying cars";
}
```

The preceding code works, even though the function is defined below the code that uses it. Function declarations are not part of the regular top-to-bottom flow of control. They are conceptually moved to the top of their scope and can be used by all the code in that scope. This is sometimes useful because it offers the freedom to order code in a way that seems the clearest, without worrying about having to define all functions before they are used.

👆 these types of functions are hoisted!

The third way to define functions is with arrow notation, like this:

```javascript
const roundTo = (n, step) => {
  let remainder = n % step;
  return n - remainder + (remainder < step / 2 ? 0 : step);
};
```

There are some nice short-hands with arrow functions to keep in mind ( one-liners, leaving out (), and empty parens) :

```javascript
const square1 = (x) => { return x _ x; };
const square2 = x => x _ x;
const horn = () => {
console.log("Toot");
};
```

Somewhat strangely, JavaScript doesn't throw an error if you pass too many arguments. For example:

```javascript
function square(x) { return x \* x; }
console.log(square(4, true, "hedgehog"));
```

Being able to reference a specific instance of a local binding in an enclosing scope—is called closure. A function that references bindings from local scopes around it is called a closure. A good mental model is to think of function values as containing both the code in their body and the environment in which they are created. When called, the function body sees the environment in which it was created, not the environment in which it is called.

Man closures are weird man. A function that returns a function...? Something like the below 👇

```javascript
function multiplier(factor) {
return number => number \* factor;
}

let twice = multiplier(2);
console.log(twice(5));
// → 10
```

Here's a good note to keep in mind when deciding when you need a function:

How difficult it is to find a good name for a function is a good indication of how clear a concept it is that you’re trying to wrap.

Some words about pure functions:

A pure function is a specific kind of value-producing function that not only has no side effects but also doesn’t rely on side effects from other code—for example, it doesn’t read global bindings whose value might change. A pure function has the pleasant property that, when called with the same arguments, it always produces the same value (and doesn’t do anything else). A call to such a function can be substituted by its return value without changing the meaning of the code. When you are not sure that a pure function is working correctly, you can test it by simply calling it and know that if it works in that context, it will work in any context. Nonpure functions tend to require more scaffolding to test.

I think when I first started programming I used to write a lot of nonpure functions. I'm thinking about my running 100 miles project, specifically. It needed to take in data of a very specific format. Not sure this is totally avoidable when working with data tables and the like, but maybe pure functions can be something to strive for.

As a recap, the three ways to declare functions are:

```javascript
// Define f to hold a function value
const f = function(a) {
console.log(a + 2);
};

// Declare g to be a function
function g(a, b) {
return a _ b _ 3.5;
}

// A less verbose function value
let h = a => a % 3;
```

Exercises

Even / Odd Recursion

my solution:

```javascript
function isEven(n) {
if (n < 0) {
n = n \* -1
}

if (n === 0) {
return true
} else if (n === 1) {
return false
} else {
return isEven(n - 2)
}
}
```

book solution:

```javascript
function isEven(n) {
  if (n == 0) return true;
  else if (n == 1) return false;
  else if (n < 0) return isEven(-n);
  else return isEven(n - 2);
}
```

my solution is correct and roughly the same as the book, but you can tell that the book solution is more eloquent. some things i could improve on are keeping the conditionals on one line if they're so short. additionally, instead of the negative check up top i could have just tucked it in with the rest of the conditional logic.
