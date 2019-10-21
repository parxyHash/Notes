# Vanilla JS Notes

# Basic DOM

Use innerHTML for creating new elements.
Use insertAdjascentHTML for more secure.
Use textContent for inside text.

# Local Storage

Stores in brower until hard reload/localstorage.clear(). Can be used to store data that will persist through a soft refresh.
Syntax is similiar to objects with dot notation.
The read-only localStorage property allows you to access a Storage object for the Document's origin; the stored data is saved across browser sessions. localStorage is similar to sessionStorage, except that while data stored in localStorage has no expiration time, data stored in sessionStorage gets cleared when the page session ends — that is, when the page is closed.

It should be noted that data stored in either localStorage or sessionStorage is specific to the protocol of the page.

The keys and the values are always strings (note that, as with objects, integer keys will be automatically converted to strings).

# .forEach()

The forEach() method executes a provided function once for each array element.

```
var array1 = ['a', 'b', 'c'];

array1.forEach(function(element) {
  console.log(element);
});
```


# .map()

The map() method creates a new array with the results of calling a provided function on every element in the calling array.
Higher-Order function.

```
var array1 = [1, 4, 9, 16];

// pass a function to map
const map1 = array1.map(x => x * 2);

console.log(map1);
// expected output: Array [2, 8, 18, 32]
```
The map function creates a new array by calling a specific function on each element in an initial array. For example, if you have an array of strings in the form "MM-DD" that represent birthdays and you want to convert each element to be in a different format, you could use the map function to create a new array with new elements. 

```
var bdays = ['08-14', '10-04', '04-21']; 

// we want a new array where the birthdays will be in the format: MM/DD
// the elem parameter will be each element from the original array 
var bdays2 = bdays.map(function(elem) { 
  return elem.replace('-', '/');
});

console.log(bdays2); // => ['08/14', '10/04', '04/21']
```
Another simple example using the map function to round an array of numbers up in JavaScript:
```
var arr = [1.5, 2.56, 5.1, 12.33];

// round each number up in an array
var rounded = arr.map(Math.ceil);

console.log(rounded); // => [2, 3, 6, 13]
```

# .filter()

The filter() method creates a new array with all elements that pass the test implemented by the provided function.
Higher-Order function.

```
var words = ['spray', 'limit', 'elite', 'exuberant', 'destruction', 'present'];

const result = words.filter(word => word.length > 6);

console.log(result);
// expected output: Array ["exuberant", "destruction", "present"]
```

The filter function creates a new array with all elements from an original array that pass a certain functions test. For example, you can use the filter function to create a new array of only positive values, like below. The function being called takes in an argument which is the value of the current element in the array.
```
var nums = [-4, 3, 2, -21, 1];

var pos = nums.filter(function(el) {
  return el > 0;
});

console.log(pos); // => [3, 2, 1]
```
You can also, for example, filter out all objects in a data file that have incorrect or undefined values. In the example below, we filter out all elements that have an incorrect age value.
```
var data = [
  {name: 'daniel', age: 45},
  {name: 'john', age: 34},
  {name: 'robert', age: null},
  {name: 'jen', age: undefined},
  {name: null, age: undefined}
];

// dataMod will now contain only the first two objects in the data array
var dataMod = data.filter(function(el) {
  if (el.name != undefined && el.age != undefined) {  
    return true;
  }
  else { 
    return false; 
  }
});
```

# .reduce()

The reduce() method executes a reducer function (that you provide) on each element of the array, resulting in a single output value.
Higher-Order function.

```
const array1 = [1, 2, 3, 4];
const reducer = (accumulator, currentValue) => accumulator + currentValue;

// 1 + 2 + 3 + 4
console.log(array1.reduce(reducer));
// expected output: 10
```
The reduce function applies a specific function to all the elements in an array and reduces it to a single value. The reduce function has actually been used in several of the challenge solutions, one example being Mean Mode. We can use the reduce function to add up all the numbers in an array for example. The four arguments the reduce function takes are:

1) previous value
2) current value
3) current index
4) original array
```
var nums = [1, 2, 3, 4];

var sum = nums.reduce(function(prevVal, curVal, curIndex, origArr) {
  return prevVal + curVal;
});

console.log(sum); // => 10
```
# .sort()

The sort() method sorts an array alphabetically:

```
var fruits = ["Banana", "Orange", "Apple", "Mango"];
fruits.sort();        // Sorts the elements of fruits
```
The reverse() method reverses the elements in an array.

You can use it to sort an array in descending order:
```
var fruits = ["Banana", "Orange", "Apple", "Mango"];
fruits.sort();        // First sort the elements of fruits
fruits.reverse();     // Then reverse the order of the elements
```

By default, the sort() function sorts values as strings.

This works well for strings ("Apple" comes before "Banana").

However, if numbers are sorted as strings, "25" is bigger than "100", because "2" is bigger than "1".

Because of this, the sort() method will produce incorrect result when sorting numbers.

You can fix this by providing a compare function:

```
var points = [40, 100, 1, 5, 25, 10];
points.sort(function(a, b){return a - b});

//Use the same trick to sort an array descending:

var points = [40, 100, 1, 5, 25, 10];
points.sort(function(a, b){return b - a});
```
# Higher-Order functions return usage

Use return statements in array method callbacks. It’s ok to omit the return if the function body consists of a single statement returning an expression without side effects, following 8.2. eslint: array-callback-return
```
// good
[1, 2, 3].map((x) => {
  const y = x + 1;
  return x * y;
});

// good
[1, 2, 3].map((x) => x + 1);

// bad - no returned value means `acc` becomes undefined after the first iteration
[[0, 1], [2, 3], [4, 5]].reduce((acc, item, index) => {
  const flatten = acc.concat(item);
});

// good
[[0, 1], [2, 3], [4, 5]].reduce((acc, item, index) => {
  const flatten = acc.concat(item);
  return flatten;
});

// bad
inbox.filter((msg) => {
  const { subject, author } = msg;
  if (subject === 'Mockingbird') {
    return author === 'Harper Lee';
  } else {
    return false;
  }
});

// good
inbox.filter((msg) => {
  const { subject, author } = msg;
  if (subject === 'Mockingbird') {
    return author === 'Harper Lee';
  }

  return false;
});
```

# Array spreads ...

Use array spreads ... to copy arrays.
```
// bad
const len = items.length;
const itemsCopy = [];
let i;

for (i = 0; i < len; i += 1) {
  itemsCopy[i] = items[i];
}

// good
const itemsCopy = [...items];

To convert an iterable object to an array, use spreads ... instead of Array.from.

const foo = document.querySelectorAll('.foo');

// good
const nodes = Array.from(foo);

// best
const nodes = [...foo];
```
# Destructuring 

Use object destructuring when accessing and using multiple properties of an object. eslint: prefer-destructuring

Why? Destructuring saves you from creating temporary references for those properties.
```
// bad
function getFullName(user) {
  const firstName = user.firstName;
  const lastName = user.lastName;

  return `${firstName} ${lastName}`;
}

// good
function getFullName(user) {
  const { firstName, lastName } = user;
  return `${firstName} ${lastName}`;
}

// best
function getFullName({ firstName, lastName }) {
  return `${firstName} ${lastName}`;
}

Use array destructuring. eslint: prefer-destructuring

const arr = [1, 2, 3, 4];

// bad
const first = arr[0];
const second = arr[1];

// good
const [first, second] = arr;
```
Use object destructuring for multiple return values, not array destructuring.

Why? You can add new properties over time or change the order of things without breaking call sites.
```
// bad
function processInput(input) {
  // then a miracle occurs
  return [left, right, top, bottom];
}

// the caller needs to think about the order of return data
const [left, __, top] = processInput(input);

// good
function processInput(input) {
  // then a miracle occurs
  return { left, right, top, bottom };
}

// the caller selects only the data they need
const { left, top } = processInput(input);
```
# Arrow Functions

When you must use an anonymous function (as when passing an inline callback), use arrow function notation. eslint: prefer-arrow-callback, arrow-spacing

Why? It creates a version of the function that executes in the context of this, which is usually what you want, and is a more concise syntax.

Why not? If you have a fairly complicated function, you might move that logic out into its own named function expression.
```
// bad
[1, 2, 3].map(function (x) {
  const y = x + 1;
  return x * y;
});

// good
[1, 2, 3].map((x) => {
  const y = x + 1;
  return x * y;
});
```
If the function body consists of a single statement returning an expression without side effects, omit the braces and use the implicit return. Otherwise, keep the braces and use a return statement. eslint: arrow-parens, arrow-body-style

Why? Syntactic sugar. It reads well when multiple functions are chained together.
```
// bad
[1, 2, 3].map((number) => {
  const nextNumber = number + 1;
  `A string containing the ${nextNumber}.`;
});

// good
[1, 2, 3].map((number) => `A string containing the ${number + 1}.`);

// good
[1, 2, 3].map((number) => {
  const nextNumber = number + 1;
  return `A string containing the ${nextNumber}.`;
});

// good
[1, 2, 3].map((number, index) => ({
  [index]: number,
}));

// No implicit return with side effects
function foo(callback) {
  const val = callback();
  if (val === true) {
    // Do something if callback returns true
  }
}

let bool = false;

// bad
foo(() => bool = true);

// good
foo(() => {
  bool = true;
});
```
In case the expression spans over multiple lines, wrap it in parentheses for better readability.

Why? It shows clearly where the function starts and ends.
```
// bad
['get', 'post', 'put'].map((httpMethod) => Object.prototype.hasOwnProperty.call(
    httpMagicObjectWithAVeryLongName,
    httpMethod,
  )
);

// good
['get', 'post', 'put'].map((httpMethod) => (
  Object.prototype.hasOwnProperty.call(
    httpMagicObjectWithAVeryLongName,
    httpMethod,
  )
));
```
Always include parentheses around arguments for clarity and consistency. eslint: arrow-parens

Why? Minimizes diff churn when adding or removing arguments.
```
// bad
[1, 2, 3].map(x => x * x);

// good
[1, 2, 3].map((x) => x * x);

// bad
[1, 2, 3].map(number => (
  `A long string with the ${number}. It’s so long that we don’t want it to take up space on the .map line!`
));

// good
[1, 2, 3].map((number) => (
  `A long string with the ${number}. It’s so long that we don’t want it to take up space on the .map line!`
));

// bad
[1, 2, 3].map(x => {
  const y = x + 1;
  return x * y;
});

// good
[1, 2, 3].map((x) => {
  const y = x + 1;
  return x * y;
});
```
Avoid confusing arrow function syntax (=>) with comparison operators (<=, >=). eslint: no-confusing-arrow
```
// bad
const itemHeight = (item) => item.height <= 256 ? item.largeSize : item.smallSize;

// bad
const itemHeight = (item) => item.height >= 256 ? item.largeSize : item.smallSize;

// good
const itemHeight = (item) => (item.height <= 256 ? item.largeSize : item.smallSize);

// good
const itemHeight = (item) => {
  const { height, largeSize, smallSize } = item;
  return height <= 256 ? largeSize : smallSize;
};
```

Enforce the location of arrow function bodies with implicit returns. eslint: implicit-arrow-linebreak
```
// bad
(foo) =>
  bar;

(foo) =>
  (bar);

// good
(foo) => bar;
(foo) => (bar);
(foo) => (
   bar
)
```
# Various Algorithim Exercises

Return the number that only appears once in the array
```
function findUniq(arr) {
  arr.sort((a,b)=>a-b);
  return arr[0]==arr[1]?arr.pop():arr[0];
}
findUniq([ 3,3,3,10,3,3,3 ]);
```
