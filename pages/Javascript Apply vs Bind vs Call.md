- In Javascript there are three common methods for a function: apply vs bind vs call. All of these method come from `Function.prototype`, that means all of functions would have these methods.
-
- ## Bind is different
-
- Let's first talk about `bind`, because this method is different from the rest. Bind will not call a function, instead it will create a new function.
- ```javascript
  console.log(1) // normal function call
  
  const log = () => console.log(1) //make a new function called log 
  log(); // call them later. output: 1
  
  const log = console.log.bind(null, 1) // make a new function with a specified argument
  log() // output: 1
  log(2) // output: 1 2 
  
  // it's the same as
  const log = (...arg) => console.log(1, ...arg);
  
  ```
-
- ## Apply vs Call
-
- Now this is a fair comparison, not like `bind` which creates a new function, these two are calling them.
- ```javascript
  // call
  console.log.call(null, 1, 2); // output 1 2
  
  // apply
  console.log.apply(null, [1, 2]); // output 1 2
  ```
- The different is that, one is using spread operator where you can directly put the arguments, where the other one is using array as the arguments.
- > The easy way to remember which one is using array is just to recognize that the word `apply` is similar to `array` quite a bit. so `apply = array`.
-
- ## This and ThisArg
-
- Now you might be thinking what are the first argument in all of those methods? And why all of them are `null`?
-
- ```javascript
  console.log.bind(null, ...);
  console.log.apply(null, ...);
  console.log.call(null, ...);
  ```
-
- Those are the `thisArg`. It'll override or set the `this` inside the function to use what we want, in this case we don't need `this` inside the `console.log` function. Take a look at this example:
-
- ```javascript
  class MyClass {
    name = "yasa"
    sayHello() {
      console.log("hello " + this.name);
    }
  }
  
  const cls = new MyClass();
  
  cls.sayHello(); // hello yasa
  ```
-
- You see the `this` referring to MyClass object? we can override that.
-
- ```javascript
  const customThis = {
    name: "john"
  }
  
  cls.sayHello.apply(customThis) // hello john
  // because we set this = customThis
  // and this.name would mean customThis.name
  
  // you can use the other methods too
  cls.sayHello.call(customThis)
  
  cls.sayHello.bind(customThis)() // parentheses at the end to call a newly created function
  ```
-
- You can even put back the real class to it.
-
- ```javascript
  cls.sayHello.apply(cls); // hello yasa
  ```
-
- In a function or method where `this` is not being used, you can pass `null` or `undefined` value in there.
-
- ```javascript
  class MyClass {
    sayHello() {
      console.log("hello"); // there is no "this" used inside this sayHello method.
    }
  }
  
  const cls = new MyClass()
  
  cls.sayHello.call(null); // ok
  
  // same as our example with console.log
  console.log.call(null, 1);
  ```
-
- There is a difference between `this` and `thisArg`. Which I will discuss in the section below.
-
- ## Function Prototype
-
- Every methods that are defined in the `Function.prototype` will be available in every other function too.
- For example `bind` is from the `Function.prototype.bind` but we can also call `bind` in other function like `console.log` with `console.log.bind` because `console.log` itself is a function. In fact every function will have it.
- ```javascript
  function ABC() {
  }
  
  ABC.apply(null); // we have .apply method here
  ```
-
- When we use and call the `call` method directly from `Function.prototype.call`. It doesn't make sense, because basically we're calling the `Function.prototype()` as it was a function, but it's not.
-
- ```javascript
  Function.prototype.call()
  // would be the same as calling:
  Function.prototype() // doesn't work
  ```
-
- For more advance way you want to use chaining method.
-
- ## Chaining Methods (Advanced)
-
- We're going to chain method together and using `Function.prototype` directly, how does that work? let's find out.
-
- ```javascript
  Function.prototype.apply.bind
  ```
-
- When we call a function normally, we will have this kind of picture.
- ```javascript
  console.log(1);
  // 1. log() is a function.
  // 2. console is the `this`.
  // 3. 1 is the argument.
  ```
-
- Now, let's take a look with `bind`/`apply`/`call`.
-
- ```javascript
  console.log.apply(console, [3, 5]);
  // 1. log() is the function
  // 2. we set the log()'s this to console
  // 3. we set 3, 5 as arguments.
  ```
-
- Now the final boss.
-
- ```javascript
  console.log.apply.bind(console.log, console, [4, 5]);
  ```
-
- Let's see how this works.
-
- We call the `bind` on `apply`, which mean we modify the `apply` function first.
  logseq.order-list-type:: number
- `bind`'s first argument is `thisArg` and we set it to `console.log`, it means we set the underlying function of apply to be `console.log`. So **`apply`'s this = `console.log`**.
  logseq.order-list-type:: number
- The second argument of `bind` is the first argument we pass to the apply, and the second argument too, which is going to be the `apply(firstArg, secondArg)`. That means `apply(console, [4, 5])`.
  logseq.order-list-type:: number
- `apply(console, [4,5])` means we set the **`console.log`'s this to `console`**. Then we pass [4, 5] as the arguments of **`apply`'s this** which is the `console.log`.
  logseq.order-list-type:: number
-
- **Here's a simpler to understand flow:**
- Set apply's this = console.log
  logseq.order-list-type:: number
- Set apply's this' this (console.log's this) = console
  logseq.order-list-type:: number
- Set arguments
  logseq.order-list-type:: number
-
- That call is a bit redundant, because we set everything manually, it is basically the same as using `Function.prototype.apply.bind` directly.
-
- ```javascript
  Function.prototype.apply.bind(console.log, console, [4, 5]);
  
  
  log() // output 4 5
  ```
-
- Remember the first code? It prints the arguments we specified to the log() but we don't want that. We normally just use arrow function, but we can go crazy with this chaining methods.
- ```javascript
  const log = console.log.bind(null, 1)
  log(2) // output: 1 2 <-- this output the 2 too, we don't want that.
  ```
- Solution:
- ```javascript
  // normal solution:
  const log = () => console.log(1);
  log(3); // output: 1 <-- without 3. Great!
  
  // crazy solution:
  const log = Function.prototype.apply.bind(console.log, null, [1]);
  log(3); // output: 1 <-- without 3. Amazing!
  ```
-
-
-
-
- #javascript #api
-