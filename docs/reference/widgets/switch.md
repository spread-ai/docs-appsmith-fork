---
Title: Switch
Description: Switch widget reference
---

<!--
README

For guidance on how to write documenation, see https://dev.stage.spread.ai/docs/contributor/guide.html. Contact Documentation when this document is ready for review.
-->

This page provides instructions on using the Switch widget, which allows users to toggle between two states.

## Content properties

These properties are customizable options present in the property pane of the widget, allowing users to modify the widget according to their preferences.

### Label

#### Text `string`

 Sets the label on the widget.

#### Position `string`

 Allows you to choose the placement of the label. You can choose:<br />

* **Left** - Aligns the text to the left of the Switch.
* **Right** - Aligns the text to the right of the Switch.

#### Alignment `string`

Alignment refers to how a label is positioned relative to a widget. By adjusting this property, you can bring the label closer to the switch within the widget's layout.

### General

#### Default State `boolean`

Determines whether the Switch is initially set to on or off.

#### Visible `boolean`

Controls the visibility of the widget. If you turn off this property, the widget would not be visible in View Mode. Additionally, you can use JavaScript by clicking on **JS** next to the **Visible** property to conditionally control the widget's visibility.

For example, if you want to make the widget visible only when the user selects Yes from a Select widget, you can use the following JavaScript expression:

```js
{{ '{{Select1.selectedOptionValue === "Yes"}}' }}
```

#### Disabled `boolean`

Prevents users from selecting the widget. Even though the widget remains visible, user input is not permitted. Additionally, you can use JavaScript by clicking on **JS** next to the **Disabled** property to control the widget's disable state conditionally.

For example, if you want to allow only a specific user to fill the input, you can use the following JavaScript expression:

```js
{{ '{{appsmith.user.email=="john@spread.ai"?false:true}}' }}
```

#### Animate Loading `boolean`

This property controls whether the widget is displayed with a loading animation. When enabled, the widget shows a skeletal animation during the loading process. Additionally, you can control it through JavaScript by clicking on the **JS** next to the property.

#### Height `string`

This property determines how the widget's height adjusts to changes in its content. There are three available options:

* **Fixed**: Maintains a constant height for the widget, allowing you to adjust it by dragging or using the resize handle.
* **Auto Height**: The widget's height adjusts dynamically in response to changes in its content.
* **Auto Height with limits**: Same as **Auto height**, with a configurable option to set the minimum and maximum number of rows the widget can occupy.

### Events

#### onChange

Allows you to define a set of [actions](/reference/framework/global-functions.md) that would be executed in response to the switch state change.

## Style properties

Style properties allow you to change the look and feel of the widget.

#### Font color `string`

Represents the text color of the widget, specified as a [CSS color value](https://developer.mozilla.org/en-US/docs/Web/CSS/color).  It can also be manipulated programmatically using the JavaScript functions.

#### Font size `string`

Determines the font size of the label. It accepts [CSS font-size](https://developer.mozilla.org/en-US/docs/Web/CSS/font-size) values and can also be programmatically modified using JavaScript functions.

#### Emphasis `string`

Enables you to select a font style for the widget, such as bold or italic. Additionally, the font style can be programmatically modified using JavaScript functions

#### Accent color `string`

The accent color property specifies the color used to highlight the switch when it is turned on. It accepts [CSS color values](https://developer.mozilla.org/en-US/docs/Web/CSS/color) and can also be programmatically modified using JavaScript functions.

## Reference properties

These properties are not available in the property pane, but can be accessed using the dot operator in other widgets or JavaScript functions. For instance, to get the visibility status, you can use `Switch1.isVisible`.

#### isSwitchedOn `boolean`

The `isSwitchedOn` property retrieves a boolean value that indicates whether the switch is turned on. It returns `true` if the switch is `on` and `false` if it is `off`.

```js
{{ '{{Switch1.isSwitchedOn}}' }}
```

#### isDisabled `boolean`

The `isDisabled` property reflects the state of the widget's Disabled setting. It is represented by a boolean value, where true indicates that the widget is not available, and false indicates that it is enabled for user interaction.

```js
{{ '{{Switch1.isDisabled}}' }}
```

#### isVisible `boolean`

The `isVisible` property indicates the visibility state of a widget, with true indicating it is visible and false indicating it is hidden.

```js
{{ '{{Switch1.isVisible}}' }}
```

## Methods

Widget property setters enable you to modify the values of widget properties at runtime, eliminating the need to manually update properties in the editor.

These methods are asynchronous and return a [Promise](/writing-code-in-studio/using-js-promises.md). You can use the `.then()` block to ensure execution and sequencing of subsequent lines of code in Studio.

#### setVisibility (param: boolean): Promise

Sets the visibility of the widget.

```js
Switch1.setVisibility(true)
```

#### setDisabled (param: boolean): Promise

Sets the disabled state of the widget.

```js
Switch1.setDisabled(false)
```

#### setRequired (param: boolean): Promise

Sets whether the widget is required or not.

```js
Switch1.setRequired(true)
```

#### setValue (param: boolean): Promise

Sets the value to be displayed in the widget.

```js
Switch1.setValue(true)
```

#### setColor (param: string): Promise

Sets the background color of the widget.

```js
Switch1.setColor('#FF0000')
```
