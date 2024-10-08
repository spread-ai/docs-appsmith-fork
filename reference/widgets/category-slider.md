---
Title: Category Slider
Description: Category Slider widget reference
---

<!--
README

For guidance on how to write documenation, see https://dev.stage.spread.ai/docs/contributor/guide.html. Contact Documentation when this document is ready for review.
-->

This page describes the properties of the Category Slider, which allows users to make selections from a predetermined set of ascending options.

## Content properties

These properties are customizable options present in the property pane of the widget, allowing users to modify the widget according to their preferences.

### Data

#### Options `array<object>`

Allows you to set the labels and unique values for the items. You can add these labels and values directly from the user interface or use JavaScript by providing options in JSON format:

```js
[
     {
          "label": "XS",
          "value": "xs"
     },
     {
          "label": "SM",
          "value": "sm"
     },
     {
          "label": "MD",
          "value": "md"
     },
     {
          "label": "LG",
          "value": "lg"
     },
     {
          "label": "XL",
          "value": "xl"
     }
]
```

Additionally, you can display dynamic data from queries or JavaScript functions by binding the response to the **Options** property. For example, if you have a query named `fetchData`, you can bind its response using:

```js
{{ '{{fetchData.data}}' }}
```

If the query data is not in the expected format, you can use the `map()` function to transform it before passing it to the widget:

```js
{{ '{{fetchData.data.map( p => ({label: p.size, value: p.size}))}}' }}
```

#### Default value `string`

Enables you to set a default option. This option is initially selected when the widget is loaded, representing the user's default input unless modified.

To set this property, assign it a value that corresponds to the value attribute of the desired option from the **Options** property.

### Label

#### Text `string`

Sets the label on the widget.

#### Position `string`

This property allows you to configure the label's placement.

Options:

* **Left**: Aligns the label to the left side of the widget.
* **Top**: Positions the label above the widget.

#### Alignment `string`

This property is only available when you select **Left** from the Position property. It allows you to align the text to the left boundary or adjust it closer to the widget using the Right alignment option.

#### Width (in columns)`number`

This property is only available when you select **Left** from the Position property. It allows you to control the proximity of the text to the widget, determining how close or far it can be positioned.

### General

#### Tooltip `string`

Enables you to add hints or provide additional information to guide the user regarding the required input.

#### Show marks `boolean`

When enabled, this property displays the labels below the slider element within the widget.

#### Visible `boolean`

Controls the visibility of the widget. If you turn off this property, the widget would not be visible in View Mode. Additionally, you can use JavaScript by clicking on **JS** next to the **Visible** property to conditionally control the widget's visibility.

For example, if you want to make the widget visible only when the user selects "Yes" from a Select widget, you can use the following JavaScript expression:

```js
{{ '{{Select1.selectedOptionValue === "Yes"}}' }}
```

#### Disabled `boolean`

Prevents users from selecting the widget. Even though the widget remains visible, user input is not permitted. Additionally, you can use JavaScript by clicking on **JS** next to the **Disabled** property to control the widget's disable state conditionally.

For example, if you want to allow only a specific user to select the option, you can use the following JavaScript expression:

```js
{{ '{{appsmith.user.email=="john@spread.ai"?false:true}}' }}
```

#### Animate Loading `boolean`

Controls whether the widget is displayed with a loading animation. When enabled, the widget shows a skeletal animation during the loading process. Additionally, you can control it through JavaScript by clicking on the **JS** next to the property.

### Events

When the event is triggered, these event handlers can execute queries, JavaScript functions, or other [supported actions](../../reference/framework/global-functions.md).

#### onChange

Specifies one or multiple actions to be triggered when the user changes the value of the Number Slider.

## Style properties

Style properties allow you to change the look and feel of the widget.

### General

#### Size `string`

Defines the size of the slider.

Options:

* Small
* Medium
* Large

### Label styles

#### Font color `string`

Represents the text color of the widget, specified as a [CSS color value](https://developer.mozilla.org/en-US/docs/Web/CSS/color). Additionally, the font color can be programmatically modified using JavaScript functions.

#### Font size `string`

Determines the font size of the label. It accepts [CSS font-size](https://developer.mozilla.org/en-US/docs/Web/CSS/font-size) values and can also be programmatically modified using JavaScript functions.

#### Emphasis `string`

Enables you to select a font style for the widget, such as bold or italic. Additionally, the font style can be programmatically modified using JavaScript functions.

### Color

#### Fill color `string`

Represents the color of the slider, specified as a [CSS color value](https://developer.mozilla.org/en-US/docs/Web/CSS/color). Additionally, the font color can be programmatically modified using JavaScript functions.

## Reference properties

Reference properties are properties that are not available in the property pane but can be accessed using the dot operator in other widgets or JavaScript functions. They provide additional information or allow interaction with the widget programmatically. For instance, to get the visibility status, you can use `CategorySlider1.isVisible`.

#### value `string`

Allows you to access the value that has been selected with the slider.

```js
{{ '{{CategorySlider1.value}}' }}
```

#### isVisible `boolean`

The `isVisible` property indicates the visibility state of a widget, with true indicating it is visible and false indicating it is hidden.

```js
{{ '{{CategorySlider1.isVisible}}' }}
```

## Methods

Widget property setters enable you to modify the values of widget properties at runtime, eliminating the need to manually update properties in the editor.

These methods are asynchronous and return a [Promise](../../writing-code-in-studio/using-js-promises.md). You can use the `.then()` block to ensure execution and sequencing of subsequent lines of code in Studio.

#### setDisabled (param: boolean): Promise

Sets the disabled state of the widget.

```js
CategorySlider1.setDisabled(false)
```

#### setVisibility (param: boolean): Promise

Sets the visibility of the widget.

```js
CategorySlider1.setVisibility(true)
```

#### setValue (param: string): Promise

Allows you to dynamically set the value of the widget.

```js
CategorySlider1.setValue('xl')
```
