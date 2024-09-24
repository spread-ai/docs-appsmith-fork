---
title: Using dynamic queries
description: Studio allows you to use parametrized queries and dynamically create queries.
---

<!--
README

For guidance on how to write documenation, see https://dev.stage.spread.ai/docs/contributor/guide.html. Contact Documentation when this document is ready for review.
-->

Passing parameters to queries in Studio allows your application to interact with data sources dynamically. It results in a more personalized and interactive experience for users, as data can be fetched or manipulated based on user input or application state.

Studio provides flexibility for passing parameters to queries both statically with Mustache Binding Syntax and dynamically using the `run()` function. This enables applications built on Studio to react intelligently to user interactions and provide a dynamic and secure user experience. 

## Using mustache syntax for static parameters

Studio utilizes the Mustache Binding Syntax (`{{ '{{ }}' }}`) for passing static parameters to queries. You can refer to widget properties, JavaScript object variables, and application states directly within your queries using this syntax.

For example, for a query named `GetUserData`, to fetch data based on a username input from `TextInput1`:

```sql
SELECT * FROM users WHERE username =TextInput1.text}}' }}'
```

The value within `{{ '{{TextInput1.text}}' }}` is used when the query is executed.

## Passing parameters at runtime using `run()`

The `run()` function can be used where parameters need to be passed at runtime. This allows you to set parameters when an event, like a button click, occurs. When invoking the `run()` function on a query, you can pass an object containing key-value pairs. Inside the query, these can be accessed via `this.params`.

For example, when a `SubmitButton` is pressed, invoke `SubmitQuery` with a parameter:

```
{{ '{{ SubmitQuery.run({ userInput: UserInput.text }) }}' }}
```

### Accessing runtime parameters inside the query

The `this.params` object within `SubmitQuery` grants access to the passed parameters:

```sql
INSERT INTO submissions (user_input) VALUES ({{ '{{this.params.userInput}}' }})
```

This binds the value of `userInput` passed at the time of the `run()` call. Ensure the keys used in the `run()` function align with those referenced within the query. This consistency is crucial for accurate data binding.

## Handling complex data types and structures

Runtime parameters aren't limited to simple data types; objects and arrays can be used as well.

For example, when inserting user details you can Pass user details as an object when a button is selected:

```
{{ '{{
    CreateUserQuery.run({
      user: { name: UserNameInput.text, age: UserAgeInput.text },
    });
}}' }}
```

The query `CreateUserQuery` inserts data into the `users` table:

```sql
INSERT INTO users (name, age) VALUES this.params.user.name}}' }}',this.params.user.age}}' }}')
```
