---
title: How to update table data
description: How to update table data using a form and a model in Studio
---

<!--
README

For guidance on how to write documenation, see https://dev.stage.spread.ai/docs/contributor/guide.html. Contact Documentation when this document is ready for review.
-->

## Synopsis

In some case it makes sense to update table data using a form and modal. The instructions for doing that are below.

## Prerequisite knowledge

- [x] Basic understanding of how to [build Studio applications](../creating-studio-applications.md).
- [x] Access to a SPREAD Studio environment.
- [x] A **Table** widget connected to a fetch query.

## Instructions

### 1. Open modal

To open a Modal based on Table row selection, select **Add a new column** and then click on the gear icon ****⚙**️** from the column's properties pane.

### 2. Set the column types

Set the **Column type** as a button and set the **onClick** event to show the Modal. If you want the Edit column to be visible at all times, you can use the **Column freeze** property to freeze the column. The modal widget remains hidden on the canvas and only becomes visible when an event is triggered. You can access and edit the Modal widget from the entity explorer.

### 3. Create the UI

Drag a Form or a JSON Form widget within the Modal, and add the required widgets. If you prefer a custom UI, use the Form widget; for a basic form setup, use the JSON Form. Additionally, you can configure the appearance of the form using the styles properties.

### 4. Display the data

To display data from the triggered row in the table, connect the data to the widget's **Default value** property using mustache syntax `{{ '{{}}' }}`:

For example, to display the user's name, add the following code in the **Default value** property of the Input widget:

```js
{{ '{{Table1.triggeredRow.name}}' }}
// 'name' refers to the column name
```

### 5. Validate data

To validate user inputs, use properties like Regex, Valid, and Required. The submit button remains disabled until all widgets meet the defined validation criteria. For more, see [validation examples](../reference/widgets/input#regex-string) for the Input widget.

### 6. Create an update query

Create an update query using the `data` reference property of the Form widget and triggered row property of the Table widget. For example, if you have a `user` table and want to update a record based on the user's ID, you can use the following query:

```sql
-- For JSON Form: {{ '{{JSONForm1.formData.name}}' }} 

UPDATE public.users
SET 
  phone = {{ '{{Form1.data.PhoneInput1}}' }},
  email = {{ '{{Form1.data.Input1}}' }}
  dob = {{ '{{DatePicker1.formattedDate}}' }}, -- To get formatted Date
  gender = {{ '{{ Form1.data.SelectGender }}' }},
  image = {{ '{{ Form1.data.InputImageURL }}' }} -- To add image from Filepicker widget use: {FilePicker1.files[0].data}}' }}
WHERE id = {{ '{{Table1.triggeredRow.id}}' }};
```

Set the Submit Button's **onClick** event to execute the update query.

### 7.  Refresh Table and close Modal

Set the Submit Button's **onSuccess** callback to trigger the fetch query, which retrieves the updated data and displays it in the Table.

### 8. Create a new **onSuccess** callback by clicking the **+** icon and set it to close the Modal

### 9. Create a new **onSuccess** callback to show the success alert

To update data directly from the Table, see [Table Inline Editing](../reference/widgets/table-inline-editing).
