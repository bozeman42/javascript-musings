# JavaScript array methods
JavaScript has several array methods that can be used to process an array of data in various ways. Some of them have very clear use cases and some of them are a little more difficult to pin down, but provide incredible versatility.

These methods are called as a method on arrays in your code and and accept functions as arguments. The array method will call the function you pass with each element of the array. e.g.
```
const myArray = [1, 2, 3]

myArray.forEach(function(element, index, array) {
	console.log(element)
})

/* output
	1
	2
	3
*/
```

Unless otherwise stated, all of the methods ***except reduce*** take a callback in the form `function(element, index, array) {}` which will be called once for each element in the original array, where `element` is the value of the current element in the array, `index` is the 0 indexed position of the element in the array, and `array` is the array from which the method was accessed.

Often you don't need to use the index or the array, and in those cases you can just write a callback function that accepts the element of the array e.g.
`myArray.forEach(item => console.log(item))`
## .forEach(callback)
This was my entry point to array methods, as it was an easy stepping off point from the traditional `for` loops. The `forEach` method simply calls the callback function with each element. It does not return a value, and it does not use the return value of the callback in any way.
#### Use cases
The only use I would recommend for `forEach` is if you are only interested in side effects (like logging, for instance). While you *can* use `forEach` to modify values in the array I recommend against that, as there are other array methods much better suited to the task.
## .map(callback)
`.map` is used when you need an array that will have transformed values for each element in your initial array. It takes a callback exactly like the callbacks in `forEach`, but when it is called on each element from the original array, the return value of the callback will be used as the element of the new array. e.g.
```
const myArray = [1, 2, 3]
const myNewArray = myArray.map(function(element, index, array) {
	return element * 3
})

console.log(myNewArray) // [3, 6, 9]
```
#### Use cases
The most common usage in my professional work is if I have an array of objects, you can get an array that is the list of a particular property on those objects.

In general if you need an array with transformations of the values in your original array, `map` is the way to go.
```
const books = [
	{
		title: 'Flatland',
		author: 'Edwin Abbott'
	},
	{
		title: 'The Color of Magic',
		author: 'Terry Pratchett'
	},
	{
		title: 'Redwall',
		author: 'Brian Jacques'
	}
]

const titles = books.map(book => book.title)
console.log(titles) // [ 'Flatland', 'The Color of Magic', 'Redwall' ]

```
## .filter(callback)
`.filter` is used when you want a subset of your array based upon certain conditions. Filter will return a **new array** containing only the elements of your array that meet the conditions you provide in your callback function.  If the callback returns a 'truthy' value, that element will be included in the array returned by `filter`. If it returns a 'falsey' value that element will not be included in the new array. **The original array is not modified.**
```
const books = [
{
	title: 'A cool book',
	pages: 423
}, {
	title: 'Another cool book',
	pages: 54
}]

const shortBooks = books.filter(function(book) {
	return book.pages < 100
})

console.log(shortBooks)
/* output
[{
  title: 'Another cool book',
	pages: 54
}]
*/

```

#### Use cases
Any time you have an array of things and you need only some of them based upon some condition you can use `.filter`. This comes up all the time and is exceptionally useful. As an added benefit, you don't modify the original array so you still have access to all of the original data.
## `.some(callback)` and `.every(callback)`
`.some` and `.every` return boolean values depending on the return values of the callback.

The callback will be called for each element in the original array as usual.
### `.some`
`.some` will return true if the callback returns a truthy value for ANY element.
```
const passengers = [
	{
		name: 'Tim',
		isAPilot: false
	},
	{
		name: 'Sarah',
		isAPilot: true
	},
	{
		name: 'Pat',
		isAPilot: false
	}
]

const isThereAPilotOnBoard = passengers.some(passenger => {
	return passenger.isAPilot
})

const isGeorgeOnboard = passengers.some(passenger => passenger.name === 'George')

console.log(isThereAPilotOnBoard) // true
console.log(isGeorgeOnboard) // false
```
### `.every`
`.every` works very much like `.some` except that it will return true only if the callback returns a truthy value for EVERY element.
```
const concertGoers = [
	{
		name: 'Yvette',
		ready: true
	},
	{
		name: 'Martha',
		ready: true
	},
	{
		name: 'Rodger',
		ready: false
	}
]

const yallReadyForThis = concertGoers.every(rocker => rocker.ready)
const yallHaveNamesWithSixLetters = concertGoers.every(rocker => rocker.name.length === 6)

console.log(yallReadyForThis) // false
console.log(yallHaveNamesWithSixLetters) // true
```


#JavaScript #programming