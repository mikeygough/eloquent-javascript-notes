Short Circuiting of Logical Operators

The logical operators && and || handle values of different types in a peculiar way. They will convert the value on their left side to Boolean type in order to decide what to do, but depending on the operator and the result of that conversion, they will return either the original left-hand value or the right-hand value.

The || operator, for example, will return the value to its left when that value can be converted to true and will return the value on its right otherwise. This has the expected effect when the values are Boolean and does something analogous for values of other types.

```javascript
console.log(null || 'user');
// → user
console.log('Agnes' || 'user');
// → Agnes
```

We can use this functionality as a way to fall back on a default value. If you have a value that might be empty, you can put || after it with a replacement value. If the initial value can be converted to false, you’ll get the replacement instead. The rules for converting strings and numbers to Boolean values state that 0, NaN, and the empty string ("") count as false, while all the other values count as true. That means 0 || -1 produces -1, and "" || "!?" yields "!?".

The ?? operator resembles ||, but returns the value on the right only if the one on the left is null or undefined, not if it is some other value that can be converted to false. Often, this is preferable to the behavior of ||.

```javascript
console.log(0 || 100);
// → 100
console.log(0 ?? 100);
// → 0
console.log(null ?? 100);
// → 100
```

The && operator works similarly but the other way around. When the value to its left is something that converts to false, it returns that value, and otherwise it returns the value on its right.

Another important property of these two operators is that the part to their right is evaluated only when necessary. In the case of true || X, no matter what X is—even if it’s a piece of program that does something terrible—the result will be true, and X is never evaluated. The same goes for false && X, which is false and will ignore X. This is called short-circuit evaluation.

The conditional operator works in a similar way. Of the second and third values, only the one that is selected is evaluated.
