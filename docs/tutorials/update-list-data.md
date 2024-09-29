---
title: How to edit items in a List widget
description: How to edit items in a List widget in Studio
---

<!--
README

For guidance on how to write documenation, see https://dev.stage.spread.ai/docs/contributor/guide.html. Contact Documentation when this document is ready for review.
-->

## Synopsis

This page will show you how to edit items in a [List](../reference/widgets/list.md) widget. You will learn how to edit, delete, and duplicate a List item using action buttons within the widget.

## Prerequisite knowledge

- [x] Basic understanding of how to [build Studio applications](../creating-studio-applications.md).
- [x] Access to a SPREAD Studio environment.

## Instructions

### 1. Create an edit icon

Drop an **Icon** button on the **List** widget and select **edit** in **Icon** from the property pane.

### 2. Create a Modal widget

Drop a **Modal** widget on to the canvas and add the required widgets to display specific details from the List item. Rename the buttons on the Modal to `Reset` and `Update`.

### 3. Add a query

Add a new query to update the List data, for example:

```sql
UPDATE product
SET name = {{ '{{inp_addProductTitle.text}}' }},
description = {{ '{{inp_addProductDescription.text}}' }},
type = 'OTHER',
     image = {{ '{{inp_addImgUrl.text}}' }}
WHERE id = {{ '{{utils.activeEditProduct ? utils.activeEditProduct.id : ''}}' }};
```

### 4. Create a JavaScript object

Create a JS Object to run the update query, close the Modal, and fetch the updated data from the datasource.

```jsx
updateProduct: async () => {
     await updateProduct.run();
     closeModal('mdl_manageProduct');
     showAlert('Product Updated', 'success');
     getProducts.run();
}
```

### 5. Add execution action

Add **Execute a JS function** action to the **onClick** event of the `Update` button on the modal. and then add a **Show modal** action to the **onClick** event of the icon. Select the Modal created in Step 2.

### 5.1 Delete list item

To delete a list item using an icon, follow these steps add a query to delete the list item based on the [triggeredItem](../reference/widgets/list.md#triggereditem-object) property.

```sql
DELETE FROM product 
WHERE id = {{ '{{lst_products.triggeredItem.id}}' }}; 
```

Add **Execute query** action to the **onClick** event of the `Delete` button to run delete query.

### 5.2 Edit list item inline

To implement inline editing of list items using a Select widget, follow these steps:

1. Drop a Select widget to the List widget. Bind data to the widget to populate values from a specific column.
2. Create a new query to update the column value for the triggered row.

```sql
UPDATE public."product" 
SET state = {{ '{{lst_products.triggeredItem.sel_state.selectedOptionValue}}' }}'
-- Specify a valid condition here. Removing the condition may update every row in the table!
WHERE id = {{ '{{lst_products.triggeredItem.id}}' }}; 
```

3. Add an action to the **onOptionChange** event of the Select widget to run the update query.
4. Set the **On success** callback to execute the fetch query for the **List** widget to reflect the changes.
