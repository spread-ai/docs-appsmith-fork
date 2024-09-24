---
title: Using JavaScript Promises
description: How to use JS Promises within your Studio applications.
---

<!--
README

For guidance on how to write documenation, see https://dev.stage.spread.ai/docs/contributor/guide.html. Contact Documentation when this document is ready for review.
-->

This document explains how to write asynchronous JavaScript code in Studio. For more on what JavaScript Promises are, see the [Mozilla Web Docs Reference](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise).

## JavaScript Promises

JavaScript Promises helps achieve asynchronous workflows that are difficult to manage when using callbacks. Studio provides native support for JavaScript promises to make working with asynchronous operations easier. All Studio framework functions return a promise, making asynchronous workflows implementation easier and readable.

### Callbacks vs promises

To understand the difference between callbacks and promise implementation, consider an example of executing three API queries in sequence and showing a message when all the APIs have finished running successfully.

```javascript
// Using Callbacks
{{ '{{ '{{ '{{
    MockApi.run(() => {
        MockApi1.run(() => {
            MockApi2.run(() => {
                showAlert('done') 
                })
        })   
    }) 
}}' }}
```

Using promise for the same example makes the implementation more manageable and readable.

```javascript
{{ '{{ '{{ '{{
    MockApi.run()
        .then(() => MockApi1.run())
        .then(() => MockApi2.run())
        .then(() => showAlert('done'))
 }}' }}
```

### Promise methods

JavaScript promises have several built-in methods. When passing a function to `.then()` or `.catch()` always remember to pass it as a [callback](https://developer.mozilla.org/en-US/docs/Glossary/Callback\_function) function, as shown below:

```javascript
{{ '{{ '{{ '{{
  (function() {
    ❌ MockApi.run().then(showAlert(`Success`))
    //highlight-next-line
    ✅ return MockApi.run().then(() => showAlert(`Success`))
      
   })()
}}' }}
```

#### Promise.any()

[Promise.any()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/any) takes an iterable array of promises as input and returns a single promise. When one of the promises first fulfil, it returns a single promise that resolves to the value of the fulfilled promise. If you want only one action/promise to finish for further execution, you can use `Promise.any()` method.
 
```javascript
{{ '{{ '{{ '{{
(function(){
    
  return Promise.any([
        MockApi.run({ name: 1 }), // if name:1 finished early
        MockApi.run({ name: 2 })
  ]).then((res) => {
    showAlert(`Winner: ${res.args.name}`) // Alert Message showns as "Winner: 1" 
  });
})()
}}' }}
```

In this example, the function calls multiple API queries passes and parameters to each API call. `Promise.any()` receives the returned promise. And then an alert message is displayed when any of the API calls complete first and returns a fulfilled promise. The message contains the argument sent to the API, which finishes execution and returns the promise first among the API calls.

#### Promise.race()

It waits for the first settled promise, fulfilled, or rejected, to get its result. You can use `Promise.race()` when you want only one action/promise to finish the execution. 

```javascript
{{ '{{ '{{ '{{
(function(){
    return  Promise.race([
            MockApi.run({ name: 1 }),
            MockApi.run({ name: 2 })
    ]).then((res) => {
        showAlert(`Winner: ${res.args.name}`)
    });
})()
}}' }}
```

In the example the function calls multiple API queries passes and parameters to each API call. The returned Promise is passed to `Promise.race()`. An alert message is displayed when any of the API calls complete first and returns a fulfilled promise. The message contains the argument sent to the API, which completes and returns the promise first among the API calls.

#### Promise.all()

It takes an array of promises - technically any iterable but usually an array - and returns a new Promise. The array of results of the Promises becomes the result of the new Promise. If one of the promises fails (reject state), the new Promise immediately rejects and returns the same error. You can use `Promise.all()` when you want all the actions successfully finish execution.

```javascript
{{ '{{ '{{ '{{
(function(){
    let employeeNames = ["Employee 1","Employee 2"];
    // Start a bunch of calls running in parallel and store returned promise
    const calls = employeeNames.map(employeeName => MockApi.run({ name: employeeName }));
    
    // Wait for all to finish (or any to reject).
    return Promise.all(calls)
            .then(() => showAlert('Promise.all - All successful'))
            .catch(() => showAlert('Promise.all - Something went wrong'))
            .finally(() => showAlert('Promise.all - finished'))
})()
}}' }}
```

In the example the function runs the API with the employee names passed as parameters. The `calls` array stores the returned promise for each API call.An alert message appears according to the success or failure case in `Promise.all()`.

#### Promise.allSettled()

It waits for all the promises to settle, regardless of the result (resolved or rejected). You can use `Promise.allSettled()` when you want all the actions to finish first.

```javascript
{{ '{{ '{{ '{{
(function(){
  let employeeNames = ["Employee 1","Employee 2"];
  // Start a bunch of calls running in parallel and store returned promise
  const calls = employeeNames.map(employeeName => MockApi.run({ name: employeeName }));
  
  // Wait for all to resolve / reject.
  return Promise.allSettled(calls)
        .then(() => showAlert('Promise.allSettled - All successful'))
        .catch(() => showAlert('Promise.allSettled - Something went wrong'))
        .finally(() => showAlert('Promise.allSettled - finished'))
})()
}}' }}
```

In the example the function runs the API with the employee names passed as parameters. The `calls` array stores the returned promise for each API call. An alert message appears according to the success or failure case in `Promise.allSettled()`.

### Using Promises in Studio

Here are some general guidelines for using Promises in Appsmith:

* Most action triggers in Studio return promises, so you can attach a `.then()` or `await` to wait for the action before proceeding.
* All triggers are wrapped in a promise, so any missed error results in an uncaught promise error.
* Return promise with `.then()` attached to it, as shown below:

```javascript
{{ '{{ '{{ '{{
  (function() {
        // the .then only runs if a promise is returned
        return MockApi.run()
            .then(() => showAlert('success'))
    })()
}}' }}
```
* Parameters are not passed in the `.then()` argument of the `action.run()`. Only the response is passed, as shown below:

```javascript
{{ '{{ '{{ '{{
  (function() {
        // define params on top so that you can use them in the later calls
        const params = { name: "Appsmith" }
        return MockApi.run(params)
            .then((response) => {
                showAlert(`${response.length} users found in `${params.name}`)
            })
    })()
}}' }}
```

## Async/Await

The `async` and `await` keywords enable the [asynchronous](/core-concepts/writing-code/javascript-editor-beta) workflow to be written in a cleaner style, avoiding the need to configure promise chains explicitly.

### Async
Adding the `async` keyword before a function always returns a promise. Other values are wrapped in a resolved promise automatically.

### Await
The keyword `await` makes JavaScript wait until that Promise settles and returns its result. 

```javascript
{{ '{{ '{{ '{{
    (async function(){ 
        const response = await MockApi.run({ name: 'Appsmith' }); 
        await storeValue( "name", response.args.name ); 
        await showAlert(appsmith.store.name); 
    })() 
}}' }}
```

In the example run `MockApi` query with the parameter `name` as 'Appsmith' and wait for the response. Store the response in the Studio store using `storeValue()` when you get the response. On successful execution of `storeValue()`, show an alert message with the data saved in the store.
