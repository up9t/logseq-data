- There is a common confusion around Javascript ecosystem, that is Javascript vs Node.js, what is the difference between them and why can't there be just only one Javascript?
- To asnwer this, first, where do we usually execute Javascript code?
- The answer is in the Browser (Chrome/Firefox/Edge).
- We can write a piece of Javascript code in the console through the browser's devtool.
- We can also write it to a file and reference the path to our html code and to see the result, we need to open our site first through a browser.
- But we can also execute Javascript directly on a machine without installing a browser.
-
- ## Runtime VS Language
-
- Javascript is a `language`.
- Because we execute the code via the browser, we can say that the browser is the `runtime`.
- Now, if I don't want to use browser, I want execute Javascript code on my machine directly without browser, that's when you use `Node.js`. So, `Node.js` is also a `runtime`.
-
- ```mermaid
  flowchart TD
    A[Language] --> B[Runtime A]
    A --> C[Runtime B]
  ```
-
- ## Javascript API vs Runtime API
-
- Javascript API is an API that you can use no matter what runtime you use. They're independent of the runtime. You can switch runtime while using Javascript API, and it would work perfectly.
- While, Runtime API is a set of API that is dependent on the Runtime, you can only use those APIs while using that runtime only. For example, in the browser you can access `window` API or `document`, we called them Browser API, these APIs aren't available in `Node.js`.
- Same with `Node.js`, there are APIs that you can have while using it, but not available while using a browser. Because, `Node.js` runs on a machine, it has access to System API like create a new file;  execute other programs; create an HTTP server. Browser doesn't have this API, that would be security issues.
-
-
- #javascript #nodejs #runtime
-
-