
#### JavaScript is not enough - We need new pieces

##### Our core JavaScript engine has 3 main parts:
1. Tread of execution
2. Memory/variable environment
3. Call stack
##### we need to add some new components:
1. Web Browser APIs/Node background APIs
2. Promises
3. Event loop, Callback/Task, queue and micro task queue.

***
 
 JavaScript by itself doesn’t provide all the functionalities needed for web development. However, when combined with **web browsers**, it gains access to a variety of powerful features. Here are some key features enabled by the web browser:
 1. **Timing**: Functions like `setTimeout()` allow for the scheduling of code execution after a specified delay
 2. **Network Communication**: The browser provides tools such as `XMLHttpRequest` and the modern `fetch()` API, which facilitate asynchronous network requests, making it easier to retrieve and send data to and from servers.
 3. **Console Interaction**: The `console` object enables developers to log messages, errors, and other information for debugging purposes, making it easier to diagnose issues in code.
 4. **HTML DOM Manipulation**: Through the `document` object, JavaScript can interact with and manipulate the HTML Document Object Model (DOM), allowing developers to dynamically change the content and structure of web pages.

JavaScript itself is a standalone programming language and does not inherently know about functions like `setTimeout()`, `XMLHttpRequest`, `fetch()`, `console`, or `document`. These functionalities are provided by the web browser's environment, allowing JavaScript to interact with the browser and the web page.

***

### 1. **What is `setTimeout()`?**
`setTimeout()` is an asynchronous function in JavaScript that allows us to schedule a function to run after a specified delay (in milliseconds). It looks like this:
```JavaScript
setTimeout(function, delay);
```

- `function`: This is the callback function that will run once the delay is over.
- `delay`: The time (in milliseconds) that JavaScript should wait before executing the function.
**For example**
```javascript
setTimeout(() => {
  console.log("This will run after 2 seconds");
}, 2000);
```
 In the above code, the `console.log` statement will be executed after a 2-second delay.
### 2. **How Does `setTimeout()` Work?**

When you call `setTimeout()`, JavaScript:

1. **Sets a timer** in the web browser (or the environment where it's running, such as Node.js) for the specified duration.
2. After the delay is completed, **the callback function is placed into a callback queue**.
3. Once the JavaScript engine has finished running all the **synchronous code** (regular code that's currently executing), the **event loop** will move the function from the callback queue to the call stack (where functions are executed).
**Important:** If there’s still synchronous code running when the timer completes, the callback won’t execute immediately. It will wait until the **call stack** is empty.

### 3. **The Call Stack, Callback Queue, and Event Loop**

To understand asynchronous behavior, we need to explain these three components:

- **Call Stack**: This is where JavaScript executes code, one function at a time. Functions are pushed onto the call stack when they are called and popped off when completed.
    
- **Callback Queue**: This is where asynchronous callbacks (like the function passed to `setTimeout()`) wait until they can be executed. They sit here after their timers have completed.
    
- **Event Loop**: The event loop's job is to monitor the call stack and the callback queue. If the call stack is empty, the event loop takes the first function from the callback queue and pushes it onto the call stack for execution.

### 4. **The Zero Timeout (setTimeout with `0` milliseconds)**

When you set `setTimeout()` with `0` milliseconds:

```javascript
setTimeout(() => {
  console.log("This runs after synchronous code");
}, 0);
```
- Even though the timer is set to `0` milliseconds, it **doesn't execute immediately**. It still waits until **all synchronous code has finished**. This is because `setTimeout()` is still an asynchronous operation, and the callback will be added to the **callback queue**, not the call stack.

**Why?** JavaScript checks if the **call stack is empty** before processing the callback queue. The event loop doesn't move the callback to the call stack until all synchronous code is executed.

### 5. **How JavaScript Implements Asynchronous Code with `setTimeout()`**

Here’s the process:

1. **Timer Setup**: When `setTimeout()` is called, a timer is set in the browser’s environment. The timer waits for the specified time (`delay`).
    
2. **Callback Queue**: Once the timer completes, the callback function is placed into the callback queue.
    
3. **Check Call Stack**: The event loop keeps checking if the call stack is empty (meaning all synchronous code has been executed).
    
4. **Move to Call Stack**: Once the call stack is empty, the event loop moves the callback function from the callback queue to the call stack, where it is executed.