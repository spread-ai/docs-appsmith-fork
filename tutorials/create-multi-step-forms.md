---
title: How to create multi-step forms
description: Learn how to create multi-step forms in Studio.
---

<!--
README

For guidance on how to write documenation, see https://dev.stage.spread.ai/docs/contributor/guide.html. Contact Documentation when this document is ready for review.
-->

This page shows you how to create a multi-step form using the [Tabs](../reference/widgets/tabs.md) widget, which allows you to collect user input over multiple steps.

## Prerequisite knowledge

- [x] Basic understanding of how to [build Studio applications](../creating-studio-applications.md).
- [x] Access to a SPREAD Studio environment.
- [x] Basic knowledge of how the [storeValue()](../reference/framework/global-functions.md#storevalue) function works.
- [x] A [Tabs](../reference/widgets/tabs.md) widget.

## Instructions

### 1. Configure the Tabs

For example, if you want to set up a multi-step form with three tabs:

1. Add and rename tabs as required. For example, rename them to `BasicInfo`, `LeadInfo`, and `CompanyInfo`.
2. Drop a [Form](../reference/widgets/form.md) widget for each tab and add relevant widgets like **Input**, and **Select** inside the form.
3. To validate user inputs, use properties like **Regex**, **Valid**, and **Required**. The submit Button remains disabled until all widgets meet the defined validation criteria. For more information, see [validation examples](../reference/widgets/input.md#regex-string) for the Input widget.

### 2. Set up navigation

Follow these steps to navigate between Tabs using [storeValue()](../reference/framework/global-functions.md#storevalue) and Button widgets:

1. To navigate to the next Tab, configure the **onClick** event of the Button within each Tab to trigger the **Store value** action and specify a unique key and Tab name.

For example, On Tab 1 (`BasicInfo`), set the Submit Button's widget **onClick** event to trigger the **Store value** action and specify:  

| Field Name | Value |
|--- | --- |
| Key | `defaulttab` |
| Value | `LeadInfo` |

In this configuration, `defaulttab` acts as a unique identifier, while the `Value` field represents the name of the tab you want to navigate to: in this case the next tab is `LeadInfo`. This setup stores the next Tab's name in the `defaulttab` key, which can then be used for navigation in subsequent steps.

2. Similarly, to navigate to the previous tab, add a new Button widget to each tab and configure the **onClick** event to trigger the **Store value** action and specify the same unique key. For example, on Tab 2 (`LeadInfo`) tab, add a new Button widget and configure its **onClick** event to allow users to go back to the previous tab. For this, select **Store value** option from the action selector and specify:

| Field Name | Value |
| --- | --- |
| Key | `defaulttab` |
| Value | `BasicInfo` |

In this configuration, the same `defaulttab` key is used to store the name of the previous tab: in this case this is `BasicInfo`. This setup stores the previous Tab's name in the `defaulttab` key, which can then be used for navigation in subsequent steps. Similarly, for each Tab, configure two Button widgets - one for navigating to the next tab and another for navigating to the previous tab.

4. To display the Tab based on the `storeValue`, add the following code into the **Default Tab** property of the Tabs widget:

```js
{{ '{{appsmith.store.defaulttab}}' }}
```

This allows you to access the Tab name from the store using the `defaulttab` key.

5. Configure the final submit Button's **onClick** event to execute the update query. For more information, see [How to submit Form data](submit-form-data.md).

6. Disable the **Show Tabs** property to hide tabs, which prevents manual selection and ensures controlled navigation. With this setup, you can navigate between Tabs using Button widgets and the `storeValue` function. You can customize the style of your Tabs by adding Buttons and Progress bar. Additionally, use the Setter methods to configure the UI elements according to your preferences.

### 3. Save partial data

To persistently store data while users are in the process of filling out the form, you have two options:

* Using the `storeValue` function to store data locally, so users can resume their form-filling journey even if they navigate away. The data gets inserted into the datasource only when the submit button is triggered.
* Direct server or datasource saving to ensure real-time  storage of user data, which can be beneficial for immediate updates or back-end integration.

For partial data saving using API, follow these steps:

1. Set up an API endpoint to handle the initial insertion of data on `Next` button's **onClick** event. In this step, save the details that are already filled out in the form, and set the rest of the fields as null or with default values. For example, to insert data, add the following into the JSON body of the REST API.

```js
{
     "name": {{ '{{user_name.text ? user_name.text : null}}' }},
     "role": {{ '{{user_role.text ? user_role.text : null}}' }},
     "lead_date": {{ '{{Date_created.formattedDate ? Date_created.formattedDate : null}}' }}
     // Add more fields as needed
}

```

The above code dynamically constructs a JSON object with optional properties, setting them to input field values or `null` if unavailable.

2. Following the initial data insertion, use the `storeValue` function to save the data's unique identifier or `ID`. For example, To save the `ID` upon the successful execution of the API, add the following code in the **onClick** event of the Next button:

```js
{{ '{{user_api.run().then(() => {
     storeValue('userid', Api1.data.id);
});}}' }}
```

3. Create a new API to update the existing record with additional data as the user advances through the form. Trigger this API execution when the user clicks on the **Next** buttons. For example, consider using the `PATCH` method, which is designed for partial updates:

```js
https://yourapi.de/api/users/{{ '{{appsmith.store.userid}}' }}
```

And in the content body pass the input data:

```js
{
     "company_name": {{ '{{company_name.text ? company_name.text : null}}' }},
     "product_name": {{ '{{product_name.text ? product_name.text : null}}' }},
          // Add more fields as needed
}

```

4. When the user completes the form and clicks the final **Submit** button, trigger an API to send the remaining or updated data to the server. With this setup, data is directly saved to the server as users click on the Next button. Additionally, you can implement functions to check tab status, open relevant tabs on login, and dynamically fetch and display stored data.
