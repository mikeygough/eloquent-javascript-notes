another way to open the console:
cmd + opt + i

to convert types:
Number()
Number.isNaN()
String()
Bool()

A do loop is a control structure similar to a while loop. It differs only on one point: a do loop always executes its body at least once, and it starts testing whether it should stop only after that first execution. To reflect this, the test appears after the body of the loop:

```javascript
let yourName;
do {
  yourName = prompt('Who are you?');
} while (!yourName);
console.log('Hello ' + yourName);
```

This program will force you to enter a name. It will ask again and again until it gets something that is not an empty string. Applying the ! operator will convert a value to Boolean type before negating it, and all strings except "" convert to true. This means the loop continues going round until you provide a non-empty name.

The for loop:

```javascript
for (let number = 0; number <= 12; number = number + 2) {
  console.log(number);
}
// → 0
// → 2
// … etcetera
```

The break statement has the effect of immediately jumping out of the enclosing loop. Its use is demonstrated in the following program, which finds the first number that is both greater than or equal to 20 and divisible by 7:

```javascript
for (let current = 20; ; current = current + 1) {
  if (current % 7 == 0) {
    console.log(current);
    break;
  }
}
// → 21
```

👆 i didn't know that you could exclude the conditional check inside of loops like this...

The continue keyword is similar to break in that it influences the progress of a loop. When continue is encountered in a loop body, control jumps out of the body and continues with the loop’s next iteration.

There is a construct called switch that is intended to express such a “dispatch” in a more direct way. Here is an example:

```javascript
switch (prompt('What is the weather like?')) {
  case 'rainy':
    console.log('Remember to bring an umbrella.');
    break;
  case 'sunny':
    console.log('Dress lightly.');
  case 'cloudy':
    console.log('Go outside.');
    break;
  default:
    console.log('Unknown weather type!');
    break;
}
```

You may put any number of case labels inside the block opened by switch. The program will start executing at the label that corresponds to the value that switch was given, or at default if no matching value is found. It will continue executing, even across other labels, until it reaches a break statement. In some cases, such as the "sunny" case in the example, this can be used to share some code between cases (it recommends going outside for both sunny and cloudy weather). Be careful, though—it is easy to forget such a break, which will cause the program to execute code you do not want executed.

interestingly here, if the user types in 'sunny' the code continues to process and will console.log both 'dress lightly' and 'go outside.'... so once a case it matched the code starts executing from there and only stops when it finds a break.

Exercises:
looping a triangle:
my solution:

```javascript
const length = 7;
for (let i = 0; i < length; i++) {
  let hashtag_output = '';
  while (hashtag_output.length <= i) {
    hashtag_output += '#';
  }
  console.log(hashtag_output);
}
```

book solution:

```javascript
for (let line = '#'; line.length < 8; line += '#') console.log(line);
```

fizzbuzz
my solution:

```javascript
const upperLimit = 100;
for (let i = 0; i < upperLimit; i++) {
  if ((i % 3 === 0) & (i % 5 === 0)) {
    console.log('FizzBuzz');
    continue;
  } else if (i % 3 === 0) {
    console.log('Fizz');
    continue;
  } else if (i % 5 === 0) {
    console.log('Buzz');
    continue;
  } else console.log(i);
}
```

book solution:

```javascript
for (let n = 1; n <= 100; n++) {
  let output = '';
  if (n % 3 == 0) output += 'Fizz';
  if (n % 5 == 0) output += 'Buzz';
  console.log(output || n);
}
```

the book solutions are so much more eloquent than mine! drastically so. damn!

chessboard
my solution:

```javascript
const size = 8;
for (let i = 0; i < size; i++) {
  let j = '';
  while (j.length < size) {
    (i + j.length) % 2 == 0 ? (j += ' ') : (j += '#');
  }
  console.log(j);
}
```

book solution:

```javascript
let size = 8;

let board = '';

for (let y = 0; y < size; y++) {
  for (let x = 0; x < size; x++) {
    if ((x + y) % 2 == 0) {
      board += ' ';
    } else {
      board += '#';
    }
  }
  board += '\n';
}

console.log(board);
```

with this one our solutions are nearly identical, though mine may be more 'cute' and harder to read!
