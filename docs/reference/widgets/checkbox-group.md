---
Title: Checkbox Group
Description: Checkbox Group widget reference
---

<!--
README

For guidance on how to write documenation, see https://dev.stage.spread.ai/docs/contributor/guide.html. Contact Documentation when this document is ready for review.
-->

This page provides instructions on using the Checkbox Group widget to allow users to select multiple items from a predefined set of choices.

## Content properties

These properties are customizable options present in the property pane of the widget, allowing users to modify the widget according to their preferences.

### Data

#### Options `String`

This property allows you to set the labels and values for the items. You can add these labels and values directly from the user interface or use JavaScript by providing options in JSON format:

```js
[
     {
          "label": "Option1",
          "value": "OPTION1"
     },
     {
          "label": "Option2",
          "value": "OPTION2"
     }
     ...
]
```

Ensure that the values assigned to each option are unique. Additionally, you can dynamically display data by using JavaScript. For instance, you can use the `.map()` function to transform the data to the desired format:

```js
{{ '{{getdata.data.map( p => ({label: p.country, value: p.country}))}}' }}
```

#### Default Selected Values `String`

Allows you to set default options in a widget. These options are initially selected when the widget is loaded, representing the user's default input unless modified. Multiple default items can be added by providing them as an array of values. For example:

```js
[
     "OPTION1", "OPTION2"
]
```

### Label

#### Text `String`

Sets the label of the Checkbox.

#### Position `String`

This property allows you to configure the label's placement in three ways:

* **Auto**: Automatically positions the label based on the widget type and layout.
* **Left**: Aligns the label to the left side of the widget.
     * **Alignment**: You can also control the text's placement relative to the Checkbox Group. You have the choice to align it either to the **Left** boundary or closer to the Checkbox Group using the **Right** alignment option.
     * **Width**: This allows you to control the proximity of the text to the Checkbox Group, determining how close or far it can be positioned.
* **Top**: Positions the label above the widget.

### Validations

#### Required `Boolean`

This validation feature allows you to designate the Checkbox Group as a mandatory field. For instance, when the Checkbox is placed within a Form widget, enabling the Required property ensures that the Form's submit button remains disabled until the Checkbox Group is checked.

### General

#### Tooltip `String`

This feature enables you to add hints or provide additional information to guide the user regarding the required input.

#### Visible `Boolean`

This property controls the visibility of the widget. If you turn off this property, the widget would not be visible in view mode. Additionally, you can use JavaScript by clicking on `JS` next to the **Visible** property to conditionally control the widget's visibility.

#### Disabled `Boolean`

This property prevents users from selecting the widget. Even though the widget remains visible, user input is not permitted. Additionally, you can use JavaScript by clicking on `JS` next to the **Disabled** property to control the widget's disable state conditionally.

#### Inline `Boolean`

When this property is turned on, the checkbox items are displayed horizontally. However, when the property is turned off, the checkbox items are displayed in a vertical line.

#### Select All Options `Boolean`

When the property is turned on, a **Select All** item is displayed, allowing the user to select all available options with a single click.

#### Animate Loading `Boolean`

This property controls whether the widget is displayed with a loading animation. When enabled, the widget shows a skeletal animation during the loading process. Additionally, you can control it through JavaScript by clicking on the **JS** next to the property.

#### Height `String`

This property determines how the widget's height adjusts to changes in its content. There are three available options:

* **Fixed**: The height of the widget remains as set using drag and resize.
* **Auto Height**: The widget's height adjusts dynamically in response to changes in its content.
* **Auto Height with limits**: Same as **Auto height**, with a configurable option to set the minimum and maximum number of rows the widget can occupy.

### Events

#### onSelectionChange

This event defines the action that would be executed when the user selects or deselects multiple or single items in the checkbox group. It allows you to specify a list of [supported actions](../../reference/framework/global-functions.md) that can be triggered in response to the checkbox state change.

## Style properties

Style properties allow you to change the look and feel of the widget.

#### Font color `String`

Represents the text color of the widget, specified as a [CSS color value](https://developer.mozilla.org/en-US/docs/Web/CSS/color).  It can also be manipulated programmatically using the JavaScript functions.

#### Font size `String`

Determines the font size of the label. It accepts [CSS font-size](https://developer.mozilla.org/en-US/docs/Web/CSS/font-size) values and can also be programmatically modified using JavaScript functions.

#### Emphasis `String`

Enables you to select a font style for the widget, such as bold or italic. Additionally, the font style can be programmatically modified using JavaScript functions.

#### Alignment

Allows you to specify the alignment between options. This property provides options such as **None**, **Start**, **End**, **Center**, **Between**, and **Around**, which determine the spacing and arrangement of the options within the designated area.

#### Accent color `String`

Defines the accent color of the widget, which is used as the fill color for the checkbox when it is checked. It accepts [CSS color values](https://developer.mozilla.org/en-US/docs/Web/CSS/color) and can also be programmatically modified using JavaScript functions.

#### Border radius `String`

Applies rounded corners to the outer edge of the widget. If JavaScript is enabled, you can specify valid [CSS border-radius](https://developer.mozilla.org/en-US/docs/Web/CSS/border-radius) to adjust the radius of the corners.

## Reference properties

These properties are not available in the property pane, but can be accessed using the dot operator in other widgets or JavaScript functions. For instance, to get the visibility status, you can use `CheckboxGroup1.isVisible`.

#### options `Array`

The `options` property is an array that contains the values of all the available options.

#### selectedValues `Array`

The `selectedValues` property holds an array of values that represents the options selected by the user.

#### isValid `Boolean`

The valid property indicates the validation status of a widget, providing information on whether the widget's current value is considered valid or not.

#### isDisabled `Boolean`

The `isDisabled` property indicates the disabled status of a widget. It is represented by a boolean value, where true indicates that the widget is not available, and false indicates that it is enabled for user interaction.

#### isVisible `Boolean`

The `isVisible` property indicates the visibility state of a widget, with true indicating it is visible and false indicating it is hidden.

## Methods

Widget property setters enable you to modify the values of widget properties at runtime, eliminating the need to manually update properties in the editor.

These methods are asynchronous and return a [Promise](/writing-code-in-studio/using-js-promises.md). You can use the `.then()` block to ensure execution and sequencing of subsequent lines of code in Studio.

#### setVisibility (param: boolean): Promise

Sets the visibility of the widget.

```js
CheckboxGroup1.setVisibility(true)
```

#### setDisabled (param: boolean): Promise

Sets the disabled state of the widget.

```js
CheckboxGroup1.setDisabled(false)
```

#### setValue (param: object): Promise

Allows you to dynamically set the value of the widget.

```js
CheckboxGroup1.setValue({ label: 'Option 2', value: 'option2' })
```

#### setRequired (param: boolean): Promise

Sets whether the widget is required or not.

```js
CheckboxGroup1.setRequired(true)
```
