---
Title: Query object
Description: A primer on the global query object in Studio.
---

<!--
README

For guidance on how to write documenation, see https://dev.stage.spread.ai/docs/contributor/guide.html. Contact Documentation when this document is ready for review.
-->

The `query` object has the parameters required to run queries and access the query data.

## Properties

The query object has the following properties that you can use to reference the query's response or check the status of the query.

### data `Array`

`data` is a read-only property that has the response body from the last successful execution of this query.

```
{{Query1.data}}
```

If this property is referenced in a widget's property field, the query is automatically run on page load. You can manually enable a query to run on page load from the query settings.

### responseMeta `object`

The `responseMeta` object has details about the response, such as the status code, headers, and other relevant information related to the query's execution and the server's response.

```
{{Query1.responseMeta}}
```

## Methods

Query object has the following methods that enable you to run a query or clear a query response.

### query.run()

When you call the `run()` function of a query, it executes the query.

#### Signature

```
run(params: Object): Promise<data>
```

| Argument | Description |
| --- | --- |
| **params** | An object containing key-value pairs to pass into the query. You can access it using the key: `{{ this.params.KEY_NAME }}`. |

The `run()` function is an asynchronous function that returns a promise and thus sequential code may not have the updated response of the query. Sequential code can be executed using the `.then()` and `.catch()` methods or the `async/await` syntax. The run function can't be invoked inside widget data properties but can be invoked from event handlers such as onClick.

```javascript title="Using promise syntax to chain actions in sequence"
{{
    Query1.run(params)
        .then((response) => {...}) // (1)!
        .catch(() => {...}) // (2)!
}}
```

1. Run after the query is successful.
2. Run when the query is succesful.

In certain scenarios, such as when running a query inside a loop, it may be necessary to pass parameters to the query with values that are contextual to the execution.

### query.clear()

This function clears all data from the query's `data` property.

```
{{Query1.clear()}}
```
