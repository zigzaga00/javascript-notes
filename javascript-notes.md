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

