---
Title: Phone Input
Description: Phone Input widget reference
---

<!--
README

For guidance on how to write documenation, see https://dev.stage.spread.ai/docs/contributor/guide.html. Contact Documentation when this document is ready for review.
-->

This page provides information on using the Phone Input, which allows you to capture phone numbers as input from users.

## Content properties

These properties are customizable options present in the property pane of the widget, allowing users to modify the widget according to their preferences.

### Data

#### Default Value `string`

Allows you to assign an initial value to the widget before user interaction.

#### Default country code `string`

Allows you to select a country code from a list of countries. Additionally, by clicking on **JS**, you can use custom country dial codes like `+27`.

#### Change country code `boolean`

Enabling this property allows the user to change the country code from the dropdown menu.

### Label

#### Text `string`

Sets the label on the widget.

#### Position `string`

This property allows you to configure the label's placement.

Options:

* **Auto**: Automatically positions the label based on the widget type and layout.
* **Left**: Aligns the label to the left side of the widget.
* **Top**: Positions the label above the widget.

#### Alignment `string`

This property is only available when you select **Left** from the Position property. It allows you to align the text to the left boundary or adjust it closer to the widget using the Right alignment option.

#### Width `number`

This property is only available when you select **Left** from the Position property. It allows you to control the proximity of the text to the widget, determining how close or far it can be positioned.

### Validations

#### Required `boolean`

When enabled, this property makes the Phone Input a mandatory field. When the Phone Input is placed within a Form widget, enabling the **Required** property ensures that the Form's submit button remains disabled until the Phone Input has some value.

#### Regex `regExp`

The **Regex** property, short for Regular Expression, enables you to apply custom validations on user input by defining specific constraints using regular expressions. If the user enters a value that does not adhere to the specified pattern, the widget displays an error message indicating `"invalid input"`.

For instance, if you want to validate that a phone number consists of exactly 10 digits, you can set the **Regex** as:

```js
^\d{10}$
```

#### Valid `boolean`

Allows you to set an expression to determine the validity of the user's input. When the specified expression evaluates to false, indicating that the input is invalid, the widget displays an error message. This feature enables you to define custom validation rules and provide informative error messages to guide the user when their input does not meet the required criteria.

#### Error Message `string`

Allows you to customize the feedback provided to the user when they enter an incorrect value. By default, the input widget displays a generic `"invalid input"` message.

### General

#### Tooltip `string`

Enables you to add hints or provide additional information to guide the user regarding the required input.

#### Placeholder `string`

Allows you to set the placeholder text displayed within the input box. This can be used to provide a hint or example value to the user, guiding them on the expected format or content of the input.

#### Visible `boolean`

Controls the visibility of the widget. If you turn off this property, the widget would not be visible in View Mode. Additionally, you can use JavaScript by clicking on **JS** next to the **Visible** property to conditionally control the widget's visibility.

For example, if you want to make the widget visible only when the user selects "Yes" from a Select widget, you can use the following JavaScript expression:

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

Controls whether the widget is displayed with a loading animation. When enabled, the widget shows a skeletal animation during the loading process. Additionally, you can control it through JavaScript by clicking on the **JS** next to the property.

#### Auto Focus `boolean`

When enabled, automatically places the user's cursor in the input box upon page load, directing their attention to the input field for immediate interaction.

#### Enable formatting `boolean`

When turned on, the phone number typed into the input gets formatted based on the selected country code.

#### Height `string`

This property determines how the widget's height adjusts to changes in its content.

Options:

* **Fixed**: Maintains a constant height for the widget, allowing you to adjust it by dragging or using the resize handle.
* **Auto Height**: The widget's height adjusts dynamically in response to changes in its content.
* **Auto Height with limits**: Same as **Auto height**, with a configurable option to set the minimum and maximum number of rows the widget can occupy.

### Events

When the event is triggered, these event handlers can run queries, JavaScript code, or other [supported actions](../../reference/framework/global-functions.md).

#### onTextChanged

Specifies the actions to be executed when the input is modified.

#### onFocus

Specifies the actions to be executed when the input area is focused.

#### onBlur

Specifies the actions to be executed when the input area loses focus.

#### onSubmit

Specifies the actions to be executed when the input is submitted with the `ENTER` key.

#### Reset on submit

Clears the input value after submission.

## Style properties

Style properties allow you to change the look and feel of the widget.

#### Font color `string`

Represents the text color of the widget, specified as a [CSS color value](https://developer.mozilla.org/en-US/docs/Web/CSS/color). Additionally, the font color can be programmatically modified using JavaScript functions.

#### Font size `string`

Determines the font size of the label. It accepts [CSS font-size](https://developer.mozilla.org/en-US/docs/Web/CSS/font-size) values and can also be programmatically modified using JavaScript functions.

#### Emphasis `string`

Enables you to select a font style for the widget, such as bold or italic. Additionally, the font style can be programmatically modified using JavaScript functions.

#### Border radius `string`

Applies rounded corners to the outer edge of the widget. If JavaScript is enabled, you can specify valid [CSS border-radius](https://developer.mozilla.org/en-US/docs/Web/CSS/border-radius) to adjust the radius of the corners.

#### Box Shadow `string`

This property adds a drop shadow effect to the frame of the widget. If JavaScript is enabled, you can specify valid [CSS box-shadow](https://developer.mozilla.org/en-US/docs/Web/CSS/box-shadow) values to customize the appearance of the shadow.

## Reference properties

Reference properties are properties that are not available in the property pane but can be accessed using the dot operator in other widgets or JavaScript functions. They provide additional information or allow interaction with the widget programmatically. For instance, to get the visibility status, you can use `PhoneInput1.isVisible`.

#### countryCode `string`

The `countryCode` property stores the country code associated with the selected country.

```js
{{ '{{PhoneInput1.countryCode}}' }}
```

#### dialCode `string`

The `dialCode` property retrieves the dialing code of the selected country.

```js
{{ '{{PhoneInput1.dialCode}}' }}
```

#### text `string`

The `text` property retrieves the formatted input value of the widget.

```js
{{ '{{PhoneInput1.text}}' }}
```

#### value `string`

The `value` property retrieves the unformatted phone number, regardless of whether formatting is enabled or not.

```js
{{ '{{PhoneInput1.value}}' }}
```

#### isValid `boolean`

The `isValid` property indicates the validation status of a widget, providing information on whether the widget's current value is considered valid or not.

```js
{{ '{{PhoneInput1.isValid}}' }}
```

#### isDisabled `boolean`

The `isDisabled` property reflects the state of the widget's **Disabled** setting. It is represented by a boolean value, where true indicates that the widget is not available, and false indicates that it is enabled for user interaction.

```js
{{ '{{PhoneInput1.isDisabled}}' }}
```

#### isVisible `boolean`

The `isVisible` property indicates the visibility state of a widget, with true indicating it is visible and false indicating it is hidden.

```js
{{ '{{PhoneInput1.isVisible}}' }}
```

## Methods

Widget property setters enable you to modify the values of widget properties at runtime, eliminating the need to manually update properties in the editor.

These methods are asynchronous and return a [Promise](../../writing-code-in-studio/using-js-promises.md). You can use the `.then()` block to ensure execution and sequencing of subsequent lines of code in Studio.

#### setVisibility (param: boolean): Promise

Sets the visibility of the widget.

```js
PhoneInput1.setVisibility(true)
```

#### setDisabled (param: boolean): Promise

Sets the disabled state of the widget.

```js
PhoneInput1.setDisabled(false)
```
