---
title: How to pass parameters to an API using Studio
description: Learn how to pass parameters to your queries with the run() framework function of Studio.
---

<!--
README

For guidance on how to write documenation, see https://dev.stage.spread.ai/docs/contributor/guide.html. Contact Documentation when this document is ready for review.
-->

## Synopsis

In Studio, you can pass static parameters to queries using mustache bindings {{ `{{}}` }}. But, if you need to execute a query multiple times with dynamic parameters - such as iterating through an array of IDs and running a query to delete each record - then you will need to pass them in the `run()` function of the query.

The `run()` function in Studio empowers developers to perform dynamic and complex database operations. By passing runtime parameters and processing responses, one can create robust applications capable of handling batch processing tasks seamlessly. Always remember to handle errors gracefully and test the system under different scenarios to ensure reliability.

To pass different parameters every time a query is executed, you can leverage the [run()](/reference/framework/query-object#queryrun) function's `params` argument. Within the query, you can access the passed parameters by using the Mustache notation {{ `{{this.params.key}}` }}.

## Prerequisite knowledge

- [x] An understanding of how to [create Studio applications](../creating-studio-applications.md).
- [x] Access to a SPREAD Studio environment.
- [x] A basic understanding of how to [use JavaScript to get input field values](https://simpledev.io/lesson/get-input-value-js/).
- [x] A basic understanding of what [query parameters](https://en.wikipedia.org/wiki/Query_string) are.

## Instructions

Imagine having to delete a set of user records identified by their unique IDs. We will write a query to delete a user based on an ID and create a JavaScript function that iterates through an array of IDs to perform the deletion for each one.

### 1. Configuring the Bulk Delete Operation

Begin by writing a query named `DeleteUserById` that deletes a user record based on the passed ID:

```sql
DELETE FROM users WHERE id = {{ '{{this.params.userId}}' }}
```


### 2. Create a JavaScript object
Create a JavaScript object that will contain the utility function for bulk deletion. In the entity explorer, create a new JS Object named `UserDeletionUtils`:

```javascript
export default {
     bulkDeleteUsers: async (userIds) => { // (1)!
          const deletePromises = userIds.map((userId) => {
               return DeleteUserById.run({ userId }); // (2)!
          });

          try { // (3)!
               const results = await Promise.all(deletePromises);
               // Optional: Handle the results, such as updating the UI or notifying success
               return results;
          } catch (error) {
               // Optional: Error handling logic
               console.error("Bulk delete operation failed", error);
               throw error;
          }
     },
};
```

1. Array to store the promises from the delete operations.
2. Executing the delete query with the current `userId`.
3. Wait for all delete operations to complete.

### 3. Trigger the process
To start the bulk deletion process, trigger `UserDeletionUtils.bulkDeleteUsers` from an event in your application (like a button click):

   ```
   {{ '{{ UserDeletionUtils.bulkDeleteUsers([12, 34, 56, 78, 90]) }}' }}
   ```

   This snippet executes the `bulkDeleteUsers` function with an array of user IDs to be deleted.

Important considerations:

- Ensure that the `DeleteUserById` query correctly references the `userId` parameter.
- Be mindful of potential race conditions or limits imposed by your data source during bulk operations.
- It is critical to handle exceptions and rejections from the promises to avoid uncaught errors that could interrupt your application flow.
- If your datasource query supports a bulk delete operation, it will be more efficient to use that.
