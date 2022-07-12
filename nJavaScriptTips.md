# JavaScript Tips

## Optional chaining

Read the value of a deeply nested property, without worrying about null or undefined value

```js
if (user && user.hobbies && user.hobbies[i]) {
  hobby = users.hobbies[i].description;
}
```

```js
hobby = user?.hobbies?.[i]?.description;
```

## Array.includes

Use Array.includes method to replace very long, repeating conditional statements. Where N options are valid.

```js
if (type === "hour" || type === "day" || type === "month" || ...) {
    // much more typing required, harder to maintain
    }
```

```js
if (["hour", "day", "week", "month"].includes(type)) {
  // it's easier to add/remove/maintain
}
```

## Object destructuring

Unpack values from objects into distinct variables.

```js
function renderUser(user) {
  const firstName = user.firstName;
  const lastName = user.lstName;
  const age = user.age;
  // ...
}
```

```js
function renderUser({ firstName, lastName, age }) {
  //...
}
```

## Array descrtructuring

```js
const arr = ["19", "30", "30"];

const hours = arr[0];
const minutes = arr[1];
const seconds = arr[2];
```

```js
const arr = ["19", "30", "30"];

const [hours, minutes, seconds] = arr;
// we can also use destructuring directly
const [hours, minutes, seconds] = str.split(":");
```

## Cast to number

Use the unary operator (+) to cast any JS value to a number

```js
// Number(e.target.value) is casting string value to number
const handleChange = (e) => setValue(Number(e.target.value));
```

```js
// The unary operator is casting string value to number
const handleChange = (e) => setValue(+e.target.value);
```

## Spread operator

Use spred operator to merge properties of multiple objects.

```js
const defaultOptions = {
  disabled: true,
  fontSize: 16,
}
const config = {};
config.disabled = defaultOptions.disabled;
config.fontSize = defaultOptions.fontSize;
```

```js
const defaultOptions = {
  disabled: true,
  fontSize: 16,
}
const config = { ...defaultOptions };
```

## Character at index

You can use bracket notation to get a character by index form a string.

```js
const str = "abc";
const c = str.charAt(2);
```

```js
const str = "abc";
const c = str[2];
```

