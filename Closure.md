
- The magic of function: **Save** it once and **Use** it again and again.
- These parenthesis `()` this indicates a function is being called (function call)

- **Execution Context**: Each time you call a function using parentheses `()`, a new **execution context** is created. This context includes:
	- Local variables
	- Arguments passed to the function
	- The function's scope chain (what it can access according to lexical scoping)
	- This new context ensures that each call to the function runs independently, even if the function is called multiple times in a row.

```javascript
function greet(name) {
console.log("Hello, " + name);
}
greet("Sarah"); // Creates a new execution context for this call
greet("Mohamed"); // A separate execution context is created for this call
```
***

### Key Points about `return` in JavaScript:

- When you return **primitive types** (like `number`, `string`, `boolean`, etc.), you are returning **a copy of the value**. These types are immutable, so only the **value** gets passed back, not the memory address.
- When you return **objects** (including arrays and functions), you're returning **a reference to the object**, not a new copy. However, even in this case, what is returned is a **reference** to the value, not the memory address itself.

```javascript
function add(a, b) {
	const sum = a + b;
    return sum; // Returns the value saved in identifier sum not sum itself.
}

let result = add(3, 4);
console.log(result); // 7
```

***
however function runs independently, even if the function is called multiple times in a row, If you want your function to hold **live data between executions**, you can achieve this through **closures**.

- When you `return` the execution ends and execution created ends else 
but what if the return was a function? inner function that has access to outer function?

### Closures: Holding Data Between Function Executions

A **closure** is created when an inner function has access to variables from an outer function, even after the outer function has returned. This way, you can hold onto data between calls.

##### the variable inside outer function captured by closure and persist in memory

Here’s how it works in more detail:

1. When a function is executed, a new **execution context** is created. This includes the function’s local variables, parameters, and its surrounding (lexical) environment.
    
2. Normally, once a function completes execution, its execution context is destroyed, and the local variables are removed from memory.
    
3. **Closures** allow you to return an inner function that still has access to the variables of its outer function. These variables are not destroyed when the outer function ends because the inner function holds a reference to them.

