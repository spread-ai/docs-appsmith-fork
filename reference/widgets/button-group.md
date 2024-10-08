---
Title: Button Group
Description: Button Group widget reference
---

<!--
README

For guidance on how to write documenation, see https://dev.stage.spread.ai/docs/contributor/guide.html. Contact Documentation when this document is ready for review.
-->

This page provides information on using the Button Group widget, which allows you to create a group of buttons, including menu buttons with drop-down items.

## Content properties

These properties are customizable options present in the property pane of the widget, allowing users to modify the widget according to their preferences.

### Data

#### Buttons `string`

Specify the buttons available in the group. You can rearrange the buttons and configure them by clicking the gear icon **⚙**️. See the [Buttons](buttons.md) reference guide for configuring individual buttons in the group.

### General

#### Visible `boolean`

Controls the visibility of the widget. If you turn off this property, the widget is not visible in View Mode. Additionally, you can use JavaScript by clicking on **JS** next to the **Visible** property to control the widget's visibility conditionally.

For example, if you want to make the widget visible only when the user selects "Yes" from a Select widget, you can use the following JavaScript expression:

```js
{{ '{{Select1.selectedOptionValue === "Yes"}}' }}
```

#### Disabled `boolean`

Prevents users from selecting the widget. Even though the widget remains visible, user input is not permitted. Additionally, you can use JavaScript by clicking on **JS** next to the **Disabled** property to control the widget's disable state conditionally.

For example, if you want to allow only a specific user to select menu item, you can use the following JavaScript expression:

```js
{{ '{{appsmith.user.email=="john@spread.ai"?false:true}}' }}
```

#### Animate Loading `boolean`

Controls whether the widget is displayed with a loading animation. When enabled, the widget shows a skeletal animation during the loading process. Additionally, you can control it through JavaScript by clicking on the **JS** next to the property.

## Style properties

Style properties allow you to change the look and feel of the widget.

### General

#### Button variant `string`

Specifies the style type of the button to indicate its significance.

Options:

* **Primary**: Fills the button with color.
* **Secondary**: Adds a colored border to the button while keeping the button itself white.
* **Tertiary**: This option does not apply any specific styling changes to the button.

This property can be dynamically set using JavaScript by providing a string value of `PRIMARY`, `SECONDARY`, or `TERTIARY`.

#### Orientation `string`

Determines the arrangement of buttons in the button group, either horizontally or vertically.

### Border and shadow

#### Border radius `string`

Applies rounded corners to the outer edge of the widget. If JavaScript is enabled, you can specify valid [CSS border-radius](https://developer.mozilla.org/en-US/docs/Web/CSS/border-radius) to adjust the radius of the corners.

#### Box Shadow `string`

This property adds a drop shadow effect to the frame of the widget. If JavaScript is enabled, you can specify valid [CSS box-shadow](https://developer.mozilla.org/en-US/docs/Web/CSS/box-shadow) values to customize the appearance of the shadow.

## Reference properties

Reference properties are properties that are not available in the property pane but can be accessed using the dot operator in other widgets or JavaScript functions. They provide additional information or allow interaction with the widget programmatically. For instance, to get the visibility status, you can use `ButtonGroup1.isVisible`.

#### isVisible `boolean`

The `isVisible` property indicates the visibility state of a widget, with true indicating it is visible and false indicating it is hidden.

```js
{{ '{{ButtonGroup1.isVisible}}' }}
```

## Methods

Widget property setters enable you to modify the values of widget properties at runtime, eliminating the need to manually update properties in the editor.

These methods are asynchronous, and you can use the `.then()` block to ensure execution and sequencing of subsequent lines of code in Studio.

#### setVisibility `boolean`

Sets the visibility of the widget.

```js
ButtonGroup1.setVisibility(true)
```

To perform sequential actions, use the `.then()` block for execution.

```js
ButtonGroup1.setVisibility(true).then(() => {
  // Code to be executed after visibility is set
})

```

#### setDisabled `boolean`

Sets the disabled state of the widget.

```js
ButtonGroup1.setDisabled(false)
```

To perform sequential actions, use the `.then()` block for execution.

```js
ButtonGroup1.setDisabled(false).then(() => {
  // Code to be executed after disabled state is set
})
```
