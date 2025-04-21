https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Conditional_operator


# Conditional chains
The ternary operator is right-associative, which means it can be "chained" in the following way, similar to an if … else if … else if … else chain:

```javascript
function example() {
  return condition1 ? value1
    : condition2 ? value2
    : condition3 ? value3
    : value4;
}
```
This is equivalent to the following if...else chain.

```javascript
Conditional chains
The ternary operator is right-associative, which means it can be "chained" in the following way, similar to an if … else if … else if … else chain:

js
Copy to Clipboard
function example() {
  return condition1 ? value1
    : condition2 ? value2
    : condition3 ? value3
    : value4;
}
This is equivalent to the following if...else chain.
```
