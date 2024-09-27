---
Title: Icon Button
Description: Icon Button widget reference
---

<!--
README

For guidance on how to write documenation, see https://dev.stage.spread.ai/docs/contributor/guide.html. Contact Documentation when this document is ready for review.
-->

This page provides information on using the Icon button widget, which is useful when you need a compact button.

## Content properties

These properties are customizable options present in the property pane of the widget, allowing users to modify the widget according to their preferences.

### Basic

#### Icon `string`

Specifies the icon to be displayed on the button. Additionally, you can use **JS** to dynamically set the icon. Studio uses the icons from the [Blueprintjs](https://blueprintjs.com/docs/#icons) library.

#### onClick

Specifies the [action](/reference/framework/global-functions.md) to be performed when the user clicks on the widget.

### General

#### Tooltip `string`

Enables you to add hints or provide additional information to guide the user regarding the required input.

#### Visible `boolean`

Controls the visibility of the widget. If you turn off this property, the widget would not be visible in View Mode. Additionally, you can use JavaScript by clicking on **JS** next to the **Visible** property to conditionally control the widget's visibility.

For example, if you want to make the widget visible only when the user selects "Yes" from a Select widget, you can use the following JavaScript expression:

```js
{{ '{{Select1.selectedOptionValue === "Yes"}}' }}
```

#### Disabled `boolean`

Prevents users from selecting the widget. Even though the widget remains visible, user input is not permitted. Additionally, you can use JavaScript by clicking on **JS** next to the **Disabled** property to control the widget's disable state conditionally.

For example, if you want to allow only a specific user to click on the Icon Button, you can use the following JavaScript expression:

```js
{{ '{{appsmith.user.email=="john@spread.ai"?false:true}}' }}
```

#### Animate Loading `boolean`

This property controls whether the widget is displayed with a loading animation. When enabled, the widget shows a skeletal animation during the loading process. Additionally, you can control it through JavaScript by clicking on the **JS** next to the property.

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

### Color

#### Button color `string`

Represents the color of the button, specified as a [CSS color value](https://developer.mozilla.org/en-US/docs/Web/CSS/color). Additionally, the font color can be programmatically modified using JavaScript functions.

### Border and shadow

#### Border radius `string`

Applies rounded corners to the outer edge of the widget. If JavaScript is enabled, you can specify valid [CSS border-radius](https://developer.mozilla.org/en-US/docs/Web/CSS/border-radius) to adjust the radius of the corners.

#### Box Shadow `string`

Adds a drop shadow effect to the frame of the widget. If JavaScript is enabled, you can specify valid [CSS box-shadow](https://developer.mozilla.org/en-US/docs/Web/CSS/box-shadow) values to customize the appearance of the shadow.

## Reference properties

Reference properties are properties that are not available in the property pane but can be accessed using the dot operator in other widgets or JavaScript functions. They provide additional information or allow interaction with the widget programmatically. For instance, to get the visibility status, you can use `IconButton1.isVisible`.

#### isVisible `boolean`

The `isVisible` property indicates the visibility state of a widget, with true indicating it is visible and false indicating it is hidden.

```js
{{ '{{IconButton1.isVisible}}' }}
```

## Methods

Widget property setters enable you to modify the values of widget properties at runtime, eliminating the need to manually update properties in the editor.

These methods are asynchronous and return a [Promise](/writing-code-in-studio/using-js-promises.md). You can use the `.then()` block to ensure execution and sequencing of subsequent lines of code in Studio.

#### setVisibility (param: boolean): Promise

Sets the visibility of the widget.

```js
IconButton1.setVisibility(true)
```

#### setDisabled (param: boolean): Promise

Sets the disabled state of the widget.

```js
IconButton1.setDisabled(false)
```
