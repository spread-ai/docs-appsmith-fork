---
Title: Checkbox
Description: Checkbox widget reference
---

<!--
README

For guidance on how to write documenation, see https://dev.stage.spread.ai/docs/contributor/guide.html. Contact Documentation when this document is ready for review.
-->

This page provides instructions on using the Checkbox widget to allow users to check or clear an item.

## Content properties

These properties are customizable options present in the property pane of the widget, allowing users to modify the widget according to their preferences.

### Label

#### Text `String`

 Sets the label of the Checkbox.

#### Position `String`

 Allows you to choose the placement of the label. You can choose:

* **Left** - Aligns the text to the left of the Checkbox.
* **Right** - Aligns the text to the right of the Checkbox.

#### Alignment `String`

Alignment refers to how a label is positioned relative to a widget. By adjusting this property, you can control the visual alignment of the label within the widget's layout

### Validations

#### Required `Boolean`

This validation feature allows you to designate the Checkbox as a mandatory field. For instance, when the Checkbox is placed within a Form widget, enabling the **Required** property ensures that the Form's submit button remains disabled until the checkbox is checked.

### General

#### Default State `Boolean`

Determines the default state of the checkbox, whether it is checked or unchecked.

#### Visible `Boolean`

This property controls the visibility of the widget. If you turn off this property, the widget would not be visible in view mode. Additionally, you can use JavaScript by clicking on **JS** next to the **Visible** property to conditionally control the widget's visibility.

#### Disabled `Boolean`

This property prevents users from selecting the Checkbox widget. Even though the widget remains visible, user input is not permitted. Additionally, you can use JavaScript by clicking on **JS** next to the **Disabled** property to control the widget's disable state conditionally.

#### Animate Loading `Boolean`

This property controls whether the widget is displayed with a loading animation. When enabled, the widget shows a skeletal animation during the loading process. Additionally, you can control it through JavaScript by clicking on the **JS** next to the property.

#### Height `String`

This property determines how the widget's height adjusts to changes in its content. There are three available options:

* **Fixed**: The height of the widget remains as set using drag and resize.
* **Auto Height**: The widget's height adjusts dynamically in response to changes in its content.
* **Auto Height with limits**: Same as **Auto height**, with a configurable option to set the minimum and maximum number of rows the widget can occupy.

### Events

#### onCheckChange

This event defines the action that would be executed when the user checks or un-checks a checkbox. It allows you to specify a list of [supported actions](../../reference/framework/global-functions.md) that can be triggered in response to the checkbox state change.

## Style properties

Style properties allow you to change the look and feel of the widget.

#### Font color `String`

Represents the text color of the widget, specified as a [CSS color value](https://developer.mozilla.org/en-US/docs/Web/CSS/color).  It can also be manipulated programmatically using the JavaScript functions.

#### Font size `String`

Determines the font size of the label. It accepts [CSS font-size](https://developer.mozilla.org/en-US/docs/Web/CSS/font-size) values and can also be programmatically modified using JavaScript functions.

#### Emphasis `String`

Enables you to select a font style for the widget, such as bold or italic. Additionally, the font style can be programmatically modified using JavaScript functions

#### Accent color `String`

Defines the accent color of the widget, which is used as the fill color for the checkbox when it is checked. It accepts [CSS color values](https://developer.mozilla.org/en-US/docs/Web/CSS/color) and can also be programmatically modified using JavaScript functions.

#### Border radius `String`

Applies rounded corners to the outer edge of the widget. If JavaScript is enabled, you can specify valid [CSS border-radius](https://developer.mozilla.org/en-US/docs/Web/CSS/border-radius) to adjust the radius of the corners.

## Reference properties

These properties are not available in the property pane, but can be accessed using the dot operator in other widgets or JavaScript functions. For instance, to get the visibility status, you can use `Checkbox1.isVisible`.

#### isChecked `Boolean`

The `isChecked` property indicates whether the checkbox is currently checked or not. It is represented by a boolean value, where true signifies that the checkbox is checked, and false signifies that it is unchecked.

#### isDisabled `Boolean`

The `isDisabled` property reflects the state of the widget's **Disabled** setting. It is represented by a boolean value, where true indicates that the widget is disabled, and false indicates that it is enabled for user interaction.

#### isVisible `Boolean`

The `isVisible` property reflects the state of the widget's **Visible** setting. It is represented by a boolean value, where true indicates that the widget is visible, and false indicates that it is hidden or not displayed on the page.

## Methods

Widget property setters enable you to modify the values of widget properties at runtime, eliminating the need to manually update properties in the editor.

These methods are asynchronous and return a [Promise](../../writing-code-in-studio/using-js-promises.md). You can use the `.then()` block to ensure execution and sequencing of subsequent lines of code in Studio.

#### setVisibility (param: boolean): Promise

Sets the visibility of the widget.

```js
Checkbox1.setVisibility(true)
```

#### setDisabled (param: boolean): Promise

Sets the disabled state of the widget.

```js
Checkbox1.setDisabled(false)
```

#### setValue (param: boolean): Promise

Allows you to dynamically set the value of the Checkbox widget.

```js
Checkbox1.setValue(true)
```

#### setRequired (param: boolean): Promise

Sets whether the widget is required or not.

```js
Checkbox1.setRequired(true)
```
