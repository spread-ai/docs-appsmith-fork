---
title: Triggering UI actions using code
description: |
     Learn how to build effective actions with Studio using multiple queries and execute them in the serial, parallel or conditional manner and programming widgets for smooth user interaction.
---

<!--
README

For guidance on how to write documenation, see https://dev.stage.spread.ai/docs/contributor/guide.html. Contact Documentation when this document is ready for review.
-->

This guide shows you how to initiate and manage UI actions, which allows you to trigger multiple queries or JavaScript functions in response to user actions. They can be executed serially, in parallel, or conditionally to create complex, dynamic behaviors.

## Execute actions in a specific order

Every widget has an event listener that can be configured to perform various actions. To execute actions in a specific order, you can chain them using the action selector. You can create multiple **Events** and **OnSuccess** callbacks to trigger different actions in a series.

To execute an action:

1. In the event property section, select the **+** icon and select the action you want to execute. For instance, set the Submit Button's **onClick** event to execute a update query.
2. Set the **onSuccess** callback to perform additional actions upon successful completion of the specified action. For instance, you can use the **onSuccess** callback to execute a fetch query or to close the Modal.
3. To set up multiple **onSuccess** callbacks, select the **+** icon within the callback configuration, and select the desired actions.

You can only execute two levels of **onSuccess** callbacks from the UI. To add additional callbacks, enable JS and and add your code, such as:

```javadscript title="Example additional code"
{{ '{{update_query.run().then(() => {
  fetch_query.run();
  closeModal('Modal1');
});}}' }}
```

To learn more about Global Functions, see the [Reference](../reference/framework/widget-actions).

## Execute actions in parallel

To execute actions in parallel, you can add multiple action selectors for a specific event:

1. In the event property, select the **+** icon and select the action you want to execute. For instance, set the Submit Button's **onClick** event to execute a status change query.
2. Create a new **onClick** event by clicking the **+** icon and set it to execute another action. For instance, set it to run a query that logs the status change.

Additionally, you can enable *JS* next to events and add your code, such as:

```js title="Sample additional code"
{{ '{{update_status.run();
log_status.run();
showAlert('Update Success', 'success');}}' }}
```

You can create multiple **Events** and **OnSuccess** callbacks to trigger different actions in parallel.

## Execute actions conditionally

This section covers conditional query execution, allowing queries to be executed based on user input or based on the results of previous queries. You can enable *JS* next to the event and add your code.

### Based on user input

For example, if you want to conditionally queries execute based on the option selected in the Select widget:

```javascript
{{ '{{
  Select_Category.selectedOptionValue === 'Categories' ? fetchCategories.run() : fetchProducts.run();
}}' }}
```

In the code, if the selected option is `Categories`, it triggers the `fetchCategories` query; otherwise, it runs the `fetchProducts` query.

### Based on query response

If you want to execute a action based on the response from another query, you can enable *JS* and add your JavaScript code. Alternatively, you can create a JSObject and define a JavaScript function for the desired logic.

For example, when the user selects `Pending` from the status dropdown, the system triggers a `fetchPendingUsers`'query. Subsequently, it displays an alert based on whether there are pending users or not.

```javascript
function fetchData() {
  if (statusDropdown.selectedOptionValue === "Pending") {
    fetchPendingUsers.run(() => {
      if (fetchPendingUsers.data.length === 0) {
        showAlert("No Users Pending Approval", "info");
      } else {
        showAlert("Fetched Users", "success");
      }
    });
  } else {
    fetchApprovedUsers.run();
  }
}
```

In the event property, enable JS and call the JavaScript function:

```js
{{ '{{JSObject1.fetchData();}}' }}
```

### Disable action

To disable an action based on specific criteria, you can use *JS* in the **Disabled** property of the widget.

For example, if specific criteria are not met, you want to disable the Refund button on the customer dashboard. Enable *JS* for **Disabled** property, and add:

```js
{{ '{{
  lst_orderHistory.triggeredItem.payment_method === 'Cash On Delivery' ||
  lst_orderHistory.triggeredItem.delivery_status === "Canceled" ||
  lst_orderHistory.triggeredItem.refund >= lst_orderHistory.triggeredItem.amount
}}' }}
```

This code determines whether to disable the Refund button on the customer dashboard based on conditions related to payment method, delivery status, and refund amount.

For more on how to pass parameters at runtime, see [Using dynamic queries](using-dynamic-queries.md#passing-parameters-at-runtime-using-run).
