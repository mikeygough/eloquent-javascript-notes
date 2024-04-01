this is weird, i didn't know you could call methods using [] notation and a string...

```javascript
const myArray = [1, 2, 3];

console.log(myArray.length);
console.log(myArray['length']);
```

When using a dot, the word after the dot is the literal name of the property. When using square brackets, the expression between the brackets is evaluated to get the property name. Whereas value.x fetches the property of value named “x”, value[x] takes the value of the variable named x and uses that, converted to a string, as the property name.

creating an object:

```javascript
let day1 = {
  squirrel: false,
  events: ['work', 'touched tree', 'pizza', 'running'],
};
```

delete and in:

```javascript
let anObject = { left: 1, right: 2 };
console.log(anObject.left);
// → 1
delete anObject.left;
console.log(anObject.left);
// → undefined
console.log('left' in anObject);
// → false
console.log('right' in anObject);
// → true
```

To find out what properties an object has, you can use the Object.keys function.

```javascript
console.log(Object.keys({ x: 0, y: 0, z: 2 }));
// → ["x", "y", "z"]
```

it's weird and kind of verbose that you have to call the class, Object, to get the keys and you can't just say something like anObject.keys...

There’s an Object.assign function that copies all properties from one object into another:

```javascript
let objectA = { a: 1, b: 2 };
Object.assign(objectA, { b: 3, c: 4 });
console.log(objectA);
// → {a: 1, b: 3, c: 4}
```

👆 i think you could also just use the spread operator here as a short-hand.

a neat short-hand to keep in mind with objects is if the value has the same name as the key, you don't need to specify the key. this seems like it's related to object unpacking in a way. here's an example:

```javascript
let journal = [];

function addEntry(events, squirrel) {
  journal.push({ events, squirrel });
}
```

in the above case, journal would like like this:

```javascript
[{ events: ['x', 'y', 'z'], squirrel: true }];
```

Array Loops (2 ways):

Old Way 👇

```javascript
for (let i = 0; i < JOURNAL.length; i++) {
  let entry = JOURNAL[i];
  // Do something with entry
}
```

Modern Way (of) 👇

```javascript
for (let entry of JOURNAL) {
  console.log(`${entry.events.length} events.`);
}
```

Push / Pop/ Shift / Unshift
Additional useful array and object methods:

`push()` and `pop()` add and remove elements at the end of an array.

`unshift()` and `shift()` add and remove elements at the start of an array.

IndexOf / lastIndexOf
To search for a specific value, arrays provide an indexOf method. The method searches through the array from the start to the end and returns the index at which the requested value was found—or -1 if it wasn’t found. To search from the end instead of the start, there’s a similar method called lastIndexOf:

```javascript
console.log([1, 2, 3, 2, 1].indexOf(2));
// → 1
console.log([1, 2, 3, 2, 1].lastIndexOf(2));
// → 3
```

Both indexOf and lastIndexOf take an optional second argument that indicates where to start searching. Should be important to know here that it only returns the index of the first occurrence. For example:

```javascript
const numbers = [1, 2, 3, 4, 5, 1];
numbers.indexOf(1);
// → 0
numbers.lastIndexOf(1);
// → 5
```

Slice / Concat
Slice returns an array that has only the elements between them. The start index is inclusive, the end index exclusive. When the end index is not given, slice will take all of the elements after the start index. You can also omit the start index to copy the entire array.

Concat appends arrays together to create a new array, similar to what the + operator does for strings.

Here's an example using both:

```javascript
function remove(array, index) {
  return array.slice(0, index).concat(array.slice(index + 1));
}
console.log(remove(['a', 'b', 'c', 'd', 'e'], 2));
// → ["a", "b", "d", "e"]
```

Something neat is that both .slice() and .indexOf() work on strings as well as arrays.

When using indexOf() on a string you can pass more than when character.

Trim / ZeroPad
The trim method removes whitespace (spaces, newlines, tabs, and similar characters) from the start and end of a string:

console.log(" okay \n ".trim());
// → okay

padStart takes the desired length and padding character as arguments:

console.log(String(6).padStart(3, "0"));
// → 006

Split / Join / Repeat
You can split a string on every occurrence of another string with split and join it again with join:

```javascript
let sentence = 'Secretarybirds specialize in stomping';
let words = sentence.split(' ');
console.log(words);
// → ["Secretarybirds", "specialize", "in", "stomping"]
console.log(words.join('. '));
// → Secretarybirds. specialize. in. stomping
```

A string can be repeated with the repeat method, which creates a new string containing multiple copies of the original string, glued together:

console.log("LA".repeat(3));
// → LALALA

Rest Parameters / Spread
It can be useful for a function to accept any number of arguments.

```javascript
function max(...numbers) {
  let result = -Infinity;
  for (let number of numbers) {
    if (number > result) result = number;
  }
  return result;
}
console.log(max(4, 1, 9, -2));
// → 9
```

The rest parameter is bound to an array containing all further arguments. If there are other parameters before it, their values aren’t part of that array. When, as in max, it is the only parameter, it will hold all arguments.

You can use a similar three-dot notation to call a function with an array of arguments:

```javascript
let numbers = [5, 1, 7];
console.log(max(...numbers));
// → 7
```

This “spreads” out the array into the function call, passing its elements as separate arguments. It is possible to include an array like that along with other arguments, as in max(9, ...numbers, 2).

Square bracket array notation similarly allows the triple-dot operator to spread another array into the new array:

```javascript
let words = ['never', 'fully'];
console.log(['will', ...words, 'understand']);
// → ["will", "never", "fully", "understand"]
```

This works even in curly brace objects, where it adds all properties from another object. If a property is added multiple times, the last value to be added wins:

```javascript
let coordinates = { x: 10, y: 0 };
console.log({ ...coordinates, y: 5, z: 1 });
// → {x: 10, y: 5, z: 1}
```

useful tidbit to create a random number between 0 and 9

const randomNumber = Math.floor(Math.random() \* 10);

Destructuring
destructuring works similarly for arrays and objects.

```javascript
const [a, b, c] = [1, 2, 3];
console.log(a);
// → 1

let { name } = { name: 'Faraji', age: 23 };
console.log(name);
// → Faraji
```

Optional Property Access
When you aren’t sure whether a given value produces an object but still want to read a property from it when it does, you can use a variant of the dot notation: object?.property.

```javascript
function city(object) {
  return object.address?.city;
}
console.log(city({ address: { city: 'Toronto' } }));
// → Toronto
console.log(city({ name: 'Vera' }));
// → undefined
```

The expression a?.b means the same a.b when a isn’t null or undefined. When it is, it evaluates to undefined. This can be convenient when, as in the example, you aren’t sure that a given property exists or when a variable might hold an undefined value.

Wow I did not know this existed👆! Feels kind of ruby-like...

JSON
All property names have to be surrounded by double quotes
Only simple data expressions are allowed—no function calls, bindings, or anything that involves actual computation
No Comments
For example:

```json
{
  "squirrel": false,
  "events": ["work", "touched tree", "pizza", "running"]
}
```

JSON.stringify() / JSON.parse()
JSON.stringify and JSON.parse to convert data to and from this format. The first takes a JavaScript value and returns a JSON-encoded string. The second takes such a string and converts it to the value it encodes:

```javascript
let string = JSON.stringify({ squirrel: false, events: ['weekend'] });
console.log(string);
// → {"squirrel":false,"events":["weekend"]}
console.log(JSON.parse(string).events);
// → ["weekend"]
```

Exercises
Sum of a Range

my solution:

```javascript
function range(start, end, step = 1) {
  const values = [];
  if (start < end) {
    while (start <= end) {
      values.push(start);
      start += step;
    }
  } else {
    while (start >= end) {
      values.push(start);
      start += step;
    }
  }
  return values;
}

function sum(values) {
  let count = 0;
  for (let value of values) {
    count += value;
  }
  return count;
}

console.log(range(1, 10));
// → [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
console.log(range(5, 2, -1));
// → [5, 4, 3, 2]
console.log(sum(range(1, 10)));
// → 55
```

book solution:

```javascript
function range(start, end, step = start < end ? 1 : -1) {
  let array = [];

  if (step > 0) {
    for (let i = start; i <= end; i += step) array.push(i);
  } else {
    for (let i = start; i >= end; i += step) array.push(i);
  }
  return array;
}

function sum(array) {
  let total = 0;
  for (let value of array) {
    total += value;
  }
  return total;
}
```

interesting use of the ternary operator inside of the function declaration, i hadn't thought of that as a possibility! i also love their use of super simple & clear if statements & looping. the essence of both programs is the same, but the solution code is much cleaner.

Reversing an Array

my solution:

```javascript
function reverseArray(inputArray) {
  const reversedArray = [];
  for (let i = 1; i <= inputArray.length; i++) {
    reversedArray.push(inputArray.slice(-i)[0]);
  }
  return reversedArray;
}

function reverseArrayInPlace(inputArray) {
  const reversedArray = [];
  const length = inputArray.length;
  for (let i = 0; i < length; i++) {
    reversedArray.push(inputArray.pop());
  }
  return reversedArray;
}
```

i couldn't complete reversing the array in-place... i thought about looping through half of the array and trying to push the first element to the back and so on but couldn't get there completely. a little embarrassing.

book solution:

```javascript
function reverseArray(array) {
  let output = [];
  for (let i = array.length - 1; i >= 0; i--) {
    output.push(array[i]);
  }
  return output;
}

function reverseArrayInPlace(array) {
  for (let i = 0; i < Math.floor(array.length / 2); i++) {
    let old = array[i];
    array[i] = array[array.length - 1 - i];
    array[array.length - 1 - i] = old;
  }
  return array;
}
```

i don't actually feel that the book solutions are all that elegant here. neater than mine perhaps, but this negative looping through isn't all that nice.

A List
darn i'm so stuck here... given an array, create a (linked) list. here's how it should look:

```javascript
console.log(arrayToList([10, 20]));
// → {value: 10, rest: {value: 20, rest: null}}
```

let's say i loop through the array...

how can i create a key who's value is an object i haven't yet created? what if i start from the last element? starting from the end of the array, create an object and append it to a list. then make a loop through that list (of objects), and set the rest value of each item to the next item in the list?

this is kind of close but it isn't correct:

```javascript
function arrayToList(inputArray) {
  // create array of objects
  const arrayOfObjects = [];
  for (let i in inputArray) {
    let object = { value: inputArray[i] };
    arrayOfObjects.push(object);
  }
  console.log(arrayOfObjects);
  // add references to next object in the array
  let i = 0;
  while (i < arrayOfObjects.length - 1) {
    if (i === arrayOfObjects.length - 1) {
      arrayofObjects[i]['rest'] = null;
      i++;
    } else {
      arrayOfObjects[i]['rest'] = arrayOfObjects[i + 1];
      i++;
    }
  }
  console.log(arrayOfObjects);
}
```

book solution:

```javascript
function arrayToList(array) {
  let list = null;
  for (let i = array.length - 1; i >= 0; i--) {
    list = { value: array[i], rest: list };
  }
  return list;
}
```

wow i was so far off. just shows how much i still don't understand the fundamentals (and hence why i'm reading this book, trying to work through these problem sets).

so they do go from back to front (my intuition was correct there though i didn't code it that way). then list gets set to an object and oh interestingly it references itself on the line `rest: list`.

that's how we're able to get null as the value of rest for the last element! it feels a little recursive in that way? it's not truly recursive but the way it overwrites itself makes it feel that way.
