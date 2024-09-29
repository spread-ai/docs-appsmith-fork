---
title: Run code on page load
description: Learn how to run code when the page loads in Studio.
---

<!--
README

For guidance on how to write documenation, see https://dev.stage.spread.ai/docs/contributor/guide.html. Contact Documentation when this document is ready for review.
-->


The execution of queries and JavaScript functions on page load is essential for initializing the page state, fetching data, and preparing the UI for interaction with the user. Automatically running queries and functions provides a smooth user experience by ensuring necessary data is available right from the start.

## Prerequisite knowledge

- [x] Basic understanding of how to [build Studio applications](../creating-studio-applications.md).
- [x] Access to a SPREAD Studio environment.
- [x] Basic knowledge of JavaScript.

## Instructions

Studio intelligently determines which queries and JavaScript functions should be run on page load based on their bindings. If a query or function's response is bound to a widget's property, it will automatically be scheduled to run when the page loads. Rules of automatic scheduling:

1. **Bound to a Widget**: When a query or function is used within a widget's properties, it's assumed that the widget's display depends on the data from that query or function. Hence, it is marked to run on page load automatically.
2. **Unbound from Widget**: If a query or a function is no longer used within any widget properties, it indicates the data may not be immediately required. In such cases, Studio removes the query or function from the page load execution list.
3. **User Settings**: You have the flexibility to override default behavior. You can mark queries and functions to always run on page load by altering their settings.

Studio allows you to manually configure the execution behavior of queries and functions.

### Steps to manually configure execution behaviour

1. Navigate to the query or function you wish to configure.
2. Click on the **Settings** tab within the query or function editor.
3. Locate the **On Page Load** option and select it to mark the query or function to always run during page load.

Once you explicitly set a query or function to run on page load, Studio will respect this setting, and the system will not alter it based on bindings.


