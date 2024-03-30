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

### find()

The array method `.find()` will return the first object which matches a given condition as `true`.

This method is useful for finding data such as posts with unique id attributes or posted by specific users.

```javascript=
const comments = [
    {
        userName: 'dduck',
        comment: 'I love puddles!',
        likes: 3
    },
    {
        userName: 'mmouse',
        comment: 'Where is the cheese?',
        likes: 2
    },
    {
        userName: 'dduck',
        comment: 'Quack!',
        likes: 8
    }
]

const dduck1 = comments.find( (comment) => comment.userName.includes('dduck') )
const bestComment = comments.find( (comment) => comment.likes > 5 )
```

Another example is if a post needs to be updated - a request to do so could be sent which includes the post id - this would then need to be found before it could be updated.

### filter()

This array method creates a new array based on a *subset* of the original array. This is another key method from the *functional programing* paradigm.

```javascript=
const comments = [
    {
        userName: 'dduck',
        comment: 'I love puddles!',
        likes: 3
    },
    {
        userName: 'mmouse',
        comment: 'Where is the cheese?',
        likes: 2
    },
    {
        userName: 'dduck',
        comment: 'Quack!',
        likes: 8
    },
    {
        userName: 'mmouse',
        comment: 'I love Minnie!',
        likes: 3
    }
]

const mmouseComments = comments.filter( (comment) => comment.userName === 'mmouse' )
```

This is a very useful method and is used in many different contexts. One example is finding results from a user generated search.

```javascript=
const films = [
    {
        title: 'Rear Window',
        genre: 'thriller'
    },
    {
        title: 'The Shining',
        genre: 'horror'
    },
    {
        title: 'Die Hard',
        genre: 'action'
    },
    {
        title: 'Manhunter',
        genre: 'thriller'
    },
    {
        title: 'Rambo',
        genre: 'action'
    },
    {
        title: 'Fracture',
        genre: 'thriller'
    }
]

const query = 'thriller';
const results = films.filter( (film) => {
    const genre = film.genre.toLowerCase();
    return genre.includes( query.toLowerCase() )
})
```

### every() and some()

The `.every()` method checks if *all* the objects in an array satisfy a given *boolean* expression. The callback function used has to itself be a boolean.

```javascript=
const nums = [2, 38, 17, 56, 98, 32];

const small = nums.every( (num) => num <= 100 );
const even = nums.every( (num) => num %2 === 0 );
```

The `.some()` method is the same as `.every()` except it will return `true` if any object in the array returns as `true`.

```javascript=
const nums = [2, 38, 17, 56, 98, 32];

const large = nums.some( (num) => num > 100 );
const odd = nums.some( (num) => num %2 === 1 );
```

### reduce()

The `.reduce()` array method takes objects in an array and reduces them to a single value. This might be, for example, summing the numbers in an array or finding the total product of them.

The `.reduce()` method takes two arguments - the *accumulator* and the *current value*.

```javascript=
const nums = [1, 2, 3, 4, 5];

const numsSum = nums.reduce( (accumulator, current) => (
    accumulator + current
))

const numsProd = nums.reduce( (accumulator, current) => (
    accumulator * current
))
```

We can pass an initial value to `.reduce()` as the second argument we pass to it.

```javascript=
const nums = [1, 2, 3, 4, 5];

const newSum = nums.reduce( (accum, current) => (
    accum + current
), 100 )
```

We can also use `.reduce()` to find the minimum or maximum value in an array. In this case, we can rename *accumulator* as *min* or *max* and alter the logic inside the callback function.

```javascript=
const nums2 = [11, 2, 23, 84, 15];

const nums2Min = nums2.reduce( (min, current) => {
    if(current < min) { return current };
    return min;
})

const nums2Max = nums2.reduce( (max, current) => {
    if(current > max) { return current };
    return max;
})
```

We can also use `.reduce()` to tally objects in an array and store the results in an object by passing an empty object as the initial value and altering the logic in the callback function.

```javascript=
const gender = ['b', 'g', 'g', 'b', 'b', 'g', 'g', 'g', 'g'];

const classGender = gender.reduce( (tally, gen) => {
    if(tally[gen]) {
        tally[gen]++;
    } else {
        tally[gen] = 1;
    }
    return tally;
}, {})
```

Another way to achieve the above tally is:

```javascript=
const gender = ['b', 'g', 'g', 'b', 'b', 'g', 'g', 'g', 'g'];

const classGender = gender.reduce( (tally, gen) => {
    tally[gen] = (tally[gen] || 0) + 1;
    return tally;
}, {})
```

A more complex example of using `.reduce()` to tally objects is found in the following code which groups films by their star ratings.

```javascript=
const films = [
    {
        title: 'Rear Window',
        genre: 'thriller',
        stars: 5
    },
    {
        title: 'The Shining',
        genre: 'horror',
        stars: 4
    },
    {
        title: 'Die Hard',
        genre: 'action',
        stars: 4
    },
    {
        title: 'Manhunter',
        genre: 'thriller',
        stars: 5
    },
    {
        title: 'Rambo',
        genre: 'action',
        stars: 5
    },
    {
        title: 'Fracture',
        genre: 'thriller',
        stars: 4
    },
    {
        title: 'Snakes on a Plane',
        genre: 'action',
        stars: 1
    }
]

const filmRatings = films.reduce( (ratedFilms, film) => {
    const rating = film.stars;
    if(!ratedFilms[rating]) {
        ratedFilms[rating] = [];
    }
    ratedFilms[rating].push(film);
    return ratedFilms;
}, {})
```

