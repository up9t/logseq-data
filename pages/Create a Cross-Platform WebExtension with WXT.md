- There are multiple ways to create a webextension, one way is to use the browser extension API, but there is quite a distinction between Chrome and Firefox when it comes to the API implementation. Firefox follows the standard more than than Chrome. Because of this differentiation, we don't want to have two different codebase that implement both of the API, we can just use a library that provides an abstraction layer so it'll distribute the result into multiple distributions so our extension stays work in different browsers. We're going to use WXT for it, it is really good and having a match with the existing Frontend Library such as Vue, React and others.
-
- When it comes to Web Extension API there are three main things that you have to know. These three things contribute to the way of how you interact with the extension. For example what will be showed when the user clicked the extension in the toolbar? or you want to inject a particular UI component to the page you're currently accessing. Or how can you access something that is outside the browser.
-
- There's a tip for you if you want to make a webextension for a SPA site, for example you want to listen for the URL change, you can do that easily with WXT, just listen for an event called `wxt:locationchange` from the content context. Here's an example:
-
- ```typescript
  export default defineContentScript({
    matches: ["*://*.youtube.com/*"],
    main(context) {
      context.addEventListener(window, "wxt:locationchange", (event) => {
        handleURLChange(event.newUrl);
      });
    },
  });
  ```
-
- #web #webextension #wxt #vue #spa
-