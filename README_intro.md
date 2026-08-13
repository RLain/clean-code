# clean-code

Scrimba's Clean code course by Dylan Isreal

🔗 https://scrimba.com/introduction-to-clean-code-c025/~02

## 3 main objectives

1. Searchable code

2. Readable code

3. Understandable code

### How do we accomplish these objectives?

- Follow language standards

- Limiting scope

- Creating new variables vs reusing

- Eliminating magic numbers

- Choose a name that describes what it does, but not how it does it

- Parent or significant other test?

- When to use Long Names vs Short Names

### Magic numbers

```js
// Clean Code Variables: Challenge 2 - Magic Numbers
const time = 86400000; // What is this?

// 86400000
const millisecondsInADay = 86400000; // How did we get to this?

// 86400000
const millisecondsInADay = 60 * 60 * 24 * 1000; //Better!
```
