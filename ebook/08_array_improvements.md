# Chapter 8: Array improvements

## `Array.from()`

`Array.from()` is the first of the many new array methods that ES6 introduced.

It will take something **arrayish**, meaning something that looks like an array but it isn't, and transform it into a real array.

``` js
// our html
<div class="fruits">
  <p> Apple </p>
  <p> Banana </p>
  <p> Orange </p>
</div>

const fruits = document.querySelectorAll(".fruits p");
const fruitArray = Array.from(fruits);

console.log(fruits);
//it will return us an array containing 3 p tags [p,p,p];

//since now we are dealing with an array we can use map
const fruitNames = fruitArray.map( fruit => fruit.textContent);

console.log(fruitNames);
// ["Apple", "Banana", "Orange"]
```

We can also simplify like this:

```js
const fruits = Array.from(document.querySelectorAll(".fruits p"));
const fruitNames = fruits.map(fruit => fruit.textContent);

console.log(fruitNames);
// ["Apple", "Banana", "Orange"]
```

Now we transformed **fruits** into a real array, meaning that we can use any sort of method such as `map` on it.

`Array.from()` also takes a second argument, a `map` function so we can write:

``` js
const fruits = document.querySelectorAll(".fruits p");
const fruitArray = Array.from(fruits, fruit => {
  console.log(fruit);
  // <p> Apple </p>
  // <p> Banana </p>
  // <p> Orange </p>
  return fruit.textContent;
  // we only want to grab the content not the whole tag
});
console.log(fruitArray);
// ["Apple", "Banana", "Orange"]
```

&nbsp;

## `Array.of()`

`Array.of()` will create an array with all the arguments we pass into it.


```js
const digits = Array.of(1,2,3,4,5);
console.log(digits);

// Array [ 1, 2, 3, 4, 5];
```

&nbsp;

## `Array.find()`

`Array.find()` returns the value of the first element in the array that satisfies the provided testing function. Otherwise `undefined` is returned.

It can be useful in instances where we have a json file, maybe coming from an API from instagram or something similar and we want to grab a specific post with a specific code that identifies it.

Let's looks at a simple example to see how `Array.find()` works.

``` js
const array = [1,2,3,4,5];

let found = array.find( e => e > 3 );
console.log(found);
// 4
```

As we mentioned, it will return the **first element** that matches our condition, that's why we only got **4** and not **5**.

&nbsp;

## `Array.findIndex()`

`Array.findIndex()` will return the *index* of the element that matches our condition.

``` js
const greetings = ["hello","hi","byebye","goodbye","hi"];

let foundIndex = greetings.findIndex(e => e === "hi");
console.log(foundIndex);
// 1
```

Again, only the index of the **first element** that matches our condition is returned.

&nbsp;

## `Array.some()` & `Array.every()`

I'm grouping these two together because their use is self-explanatory: `.some()` will search if there are some items matching the condition and
stop once it finds the first one, `.every()` will check that all items match the given condition.

```js
const array = [1,2,3,4,5,6,1,2,3,1];

let arraySome = array.some( e => e > 2);
console.log(arraySome);
// true

let arrayEvery = array.every(e => e > 2);
console.log(arrayEvery);
// false
```

Simply put, the first condition is true, because there are **some** elements greater than 2, but the second is false because **not every element** is greater than 2.