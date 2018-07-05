# Gatecoin API JS client  
Gatecoin is a cryptocurrency exchange, providing a lot of functionality via REST API. 
Project goal is to create a TypeScript client library for some of the REST endpoints and provide documentation for it.
  
## Requirements  
- Three ways of usage:  
    - for Node.js: standart module import;  
    - for browser: using module bundler like Webpack, RequireJS, Browserify,  SystemJS/JSPM or Rollup;  
    - for browser: using `<script>` tag to load from the server or from CDN;  
- Browser support upto IE10;  
  
## Resources:  
Latest API documentation: https://gatecoin.com/api/  
API UI: https://api.gatecoin.com/swagger-ui/index.html  
Sandbox: https://api.gtcprojects.com/swagger-ui/index.html  
C# library: https://github.com/Gatecoin/api-gatecoin-dotnet  
  
  
## TODO  
- [ ] api mockups  
- [ ] online docs generation  
  
  
## Testing requirements  
- [ ] in browser testing  
- [ ] Node.js testing  
- [ ] API contract tests  
- [ ] client contract tests  
  
  
## Next steps  
- CI and CD pipeline  
- Integration with external bot systems  
- Maintenance  
- Examples blog  
  
  
## Architecture decisions  
It looks like a good idea to document why we decided to use these tool but not the other. Or why we chose this approach but not the other.
After some time the reasons could change so the architecture could be reviewed.  
  
1. The same code-base for Node.js and for the browsers.  
It is possible to create and support two different versions for the server-side usage (Node.js) and for the browser.
Nevertheless it looks like a good idea to use the benefit that JavaScript can be used in both worlds.  
2. TypeScript will be used for development.  
The most important reasons are:
    - the easiest way to declare user interface contract (classes, methods, parameters types);  
    - automatic documentation generation;  
    - more readable, self-explaining, error-proof and static analyzed code;  
    - possibility to use ES6, ES7 and later (instead of babel);  
More reasons could be found here: [JavaScript libraries should be written in TypeScript](https://news.ycombinator.com/item?id=11296491);  
3. [fetch()](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) instead of [XMLHttpRequest()](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest)  
In the browser code we could use standard XHR object to proceed the server requests.
To keed the code-base the same we should use [XHR polifill](https://github.com/pwnall/node-xhr2) for Node.js.
Meanwhile for the better developer experience fetch() polifill looks like a better option.  
4. [Promises](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) instead of [callback hell](http://callbackhell.com/)  
IE10 doesn't support promises so if we want to keep the browser version tiny we should struggle with XHR and standard callbacks everywhere.
From the other side:
    - IE10 is used by [less then 3% of users](https://caniuse.com/usage-table);  
    - browser [fetch](https://github.com/github/fetch) and [promise polifills](https://github.com/taylorhakes/promise-polyfill) together are about 3kb Gzipped;  
    - It could be expected that the modern developers would prefer to use Promises instead of callbacks;  
5. [pony-fills](https://ponyfill.com) instead of poly-fills  
as the first doesn't change global scope so the developers would not have unexpected unnecessary surprises.  
6. We could do packaging by ourselves or we can give the developer the opportunity to do this.  
...[to be discovered]  
7. Can we use Typescript generated UMD files for both - browser and Node?  
TypeScript can't generate UMD files with window fallback for global namespace to work under the browser.
https://github.com/Microsoft/TypeScript/issues/8436
So we have to use bundler to make a package. There are some of them:  
8. Webpack, RequireJS, Browserify,  SystemJS/JSPM, Rollup, Amdclean or uRequire?
Amdclean allows to run modules without loader and it doesn't have runtime overhead.  
...[to be discovered]  
  
  
  
