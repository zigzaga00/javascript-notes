# JavaScript Notes

## Primitive Data Types

Javascript has five main *primitive* datatypes:

- Number
- String
- Boolean
- Null
- Undefined

There are two more - Symbol and BigInt.

### Number

There is only one number datatype in js. This includes positive, negative and decimal numbers. We can perform the usual mathematical operations on number datatypes.

### String

String datatypes can be seen as strings of characters - we define them by using quotation marks.

Strings are indexed from 0 and use [] for access.

Strings have inbuilt methods such as:
- `.toUpperCase()`
- `.toLowerCase()`
- `.trim()` trims whitespace at the start and the end
- `.indexOf()`
- `.slice()` this method uses , to separate the values
- `.replace()`

Some methods accept arguments and we can chain methods together:

`.trim().replace("hello", "goodbye")`

We can use *escape* methods with strings in js.

String template literals let us embed expressions into strings - they use backticks in js and ${}

```javascript
let people = 2;
console.log(`There are ${8 + people} humans.`);
```

### Boolean

Same as in *python* - `true` or `false`

>[!NOTE]
>No capitalisation on boolean values in javascript

### Null

Similar to `None` datatype in *python* - this value needs to be set - useful if we want to assign a value to a variable later in our code.

### Undefined

This is used when no value is assigned to a variable - it is different to `null` - we can declare a variable without assigning a value to it in js.

## Variables

`var` used to be used but it is not needed anymore.

`let` is how we declare variables unless we want them to be *constants*. We declare *constants* using `const`

`let` variables can change *datatype* and *value* whereas `const` variables cannot change at all.

We can use `typeof` to find the datatype of a variable or value - `typeof` is an *operator* and not a *function* or a *method* so no `()` are needed.

## `parseInt` and `parseFloat`

We can use these functions to get the numeric value of given strings. `parseInt` will round *floats* to whole numbers - if we want the full decimal version we can use `parseFloat`

These functions can be useful when working with data input from forms as user supplied data such as this is a *string* by default.

## Arrow Functions

We can use *arrow functions* when we use *anonymous functions* aka *function expressions*.

We do not need to use the keyword `function` but we do need to use `=>` which looks like an arrow.

```javascript=
const squaredNum = (n) => {
    return n*n;
}
```

If we have only one parameter (as in the example above) we can omit the `()` but it depends on how we like to code.

```javascript=
const squaredNum = n => {
    return n*n;
}
```

We *must* include the `()` if we have more than one parameter.

```javascript=
const multiply = (x, y) => {
    return x*y;
}
```

If the function does not take any arguments, we can just use `()` as shown below.

```javascript=
const greeting = () => {
    return 'hello world!';
}
```

If we only have one expression which is returned without any other logic involved in the function, we can use *implicit return* which means we can omit the keyword `return` - in order to use this we will need to use `()` instead of `{}` for the function block.

```javascript=
const nums = [1, 2, 3, 4, 5];
const oddEven = nums.map(n => (
    n % 2 === 0 ? 'even' : 'odd'
));
```

It is possible to put arrow functions onto one line if it makes sense to do so - i.e. the logic in the function is not too long. In this case, we do not need to wrap the function in `()` or `{}`

```javascript=
const squaredNum = (n) => n*n;
```

An example using `.map()`

```javascript=
const nums = [1, 2, 3, 4, 5];
const squaredNums = nums.map( (n) => n*n );
```

## Applying Functions to Data Collections

### Array Callback Methods

Some array methods accept *callback* functions as arguments.

>[!NOTE]
>A *callback* is just a *function* which is passed to another *function* or a *method* as an *argument*

This is common in js and is possible because in js everything is an *object*.

We find this pattern in python, too - we are looking at situations such as we find in the *functional programing* paradigm in which we use *map*, *filter* and (not often) *reduce* to create new collections of data from existing *data collections*.

The general idea is that we want the *callback function* to be run on every object in the data collection - in this case *array*.

### forEach()

The `.forEach()` array method executes a *callback function* for each object in the array it is called on.

The callback can be a regular function or a *function expression* aka an *anonymous function*.

With a regular function:

```javascript=
function doubleNum(n) {
    return n * 2;
}

const numbers = [1, 2, 3, 4, 5];

numbers.forEach(doubleNum);
```

With an anonymous function:

```javascript=
const numbers = [1, 2, 3, 4, 5];

numbers.forEach(function(n) {
    console.log(n * 2);
})
```

We could achieve the same results using a *for of* loop but when we use `.forEach()` we can capture the index more easily. The `.forEach()` array method also introduces us to the idea of using callback functions on data collections.

>[!NOTE]
>We did not used to have *for of* loops in js so from a point of history `.forEach()` was used

Here is how we can capture the index:

```javascript=
const numbers = [1, 2, 3, 4, 5];

numbers.forEach(function(n, i) {
    console.log(`${i} : ${n*2}`);
})
```

### map()

A very useful array method which uses a callback function as an argument is `.map()`

This method is similar to `.forEach()` but it creates a new array based on the transformed objects from the original array. We could, for example, make a new array from an array of numbers but in the new array the numbers have been doubled.

```javascript=
const nums = [1, 2, 3, 4, 5];

const doubledNums = nums.map(function(n) {
    return n*2;
})
```

We can use regular functions as the callback but typically anonymous functions are used.

Here is another example of using `.map()` - in this one the new array will be filled with objects created from the original array.

```javascript=
const nums = [1, 2, 3, 4, 5];

const numsData = nums.map(function(n) {
    return {
        value: n,
        isEven: n % 2 === 0
    }
})
```

Here is one more example in which we create a new array which is comprised of just the *title* value of book objects in an original array:

```javascript=
const books = [
    {
        title: 'Wutherning Heights',
        author: 'Emily Bronte',
        rating: 5
    },
    {
        title: 'Jayne Ayre',
        author: 'Charlotte Bronte',
        rating: 4
    },
    {
        title: 'Metamorphosis',
        author: 'Franz Kafka',
        rating: 5
    }
]

const titles = books.map(function(book) {
    return book.title;
})
```

Since `.map()` creates a new array we need to make sure that the callback function passed to it returns values.

