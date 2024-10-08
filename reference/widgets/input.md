---
Title: Input
Description: Input widget reference
---

<!--
README

For guidance on how to write documenation, see https://dev.stage.spread.ai/docs/contributor/guide.html. Contact Documentation when this document is ready for review.
-->

This page provides information on using the Input widget to gather and validate user input such as text, numbers, emails, and passwords.

## Content properties

These properties are customizable options present in the property pane of the widget, allowing users to modify the widget according to their preferences.

### Data

#### Data type `string`

Allows you to set the type of data you want to capture in the user input, enabling the associated validation for the chosen data type.

Options:

* **Single-line text:** Accepts input with a single line of text, typically used for short responses like names or titles.
* **Multi-line text:** Allows input with multiple lines, suitable for longer text entries, such as comments or descriptions.
* **Number:** Permits input of numeric values, restricting non-numeric characters.
* **Password:** Masks the user's input to hide sensitive information like passwords or PINs.
* **Email:** Validates and accepts email addresses, ensuring they match the required format.

#### Default value `string`

Allows you to specify an initial value for the widget when it's first displayed.

### Label

#### Text `string`

Allows you to define the label on the widget.

#### Position `string`

This property allows you to configure the label's placement.

Options:

* **Auto**: Automatically positions the label based on the widget type and layout.
* **Left**: Aligns the label to the left side of the widget.
* **Top**: Positions the label above the widget.

#### Alignment `string`

This property is only available when you select **Left** from the Position property. It allows you to align the text to the left boundary or adjust it closer to the widget using the Right alignment option.

#### Width `number`

This property is only available when you select **Left** from the Position property. It allows you to control the proximity of the text to the widget, determining how close or far it can be positioned. Default value of **Width** is `5`.

### Validation

#### Required `boolean`

This validation feature allows you to designate the Input as a mandatory field. For instance, when the Input is placed within a Form widget, enabling the Required property ensures that the Form's submit button remains disabled until the Input has some value.

#### Max characters	`number`

Sets a maximum length allowed for user input. Only appears when **Data Type** is set to a Text type.

#### Regex `string`

The Regex property, short for Regular Expression, enables you to apply custom validations on user input by defining specific constraints using regular expressions. If the user enters a value that does not adhere to the specified pattern, the widget displays an error message indicating `"invalid input"`.

For instance, if you want to validate that the user enters a value in multiples of 5. You can set **Regex** as:

```js
.*[05]$
```

##### Email validation

To validate whether an entered email is correct, use the following regular expression code inside the [Regex](#regex-string) property of an Input widget:

```js
^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$
```

##### Phone number validation

To get phone number in a specific format or length, you can use the following codes:

For example, if you want to validate international phone numbers starting with a plus sign (+) and a total length between 6 and 14 digits, use the following code inside the **Regex** property:

```js
^\+(?:[0-9]●?){6,14}[0-9]$
```

##### Number validation

If you need to add number validation for fields like currency or prices, you can use the following regular expression code inside the **Regex** property of any Input widget:

```js
^(0*100(\.0*)?)$|^([1-9]?[0-9](\.\d*)?)$ // (1)! 
^[1-9][0-9]*$ // (2)!
^-?\d+(\.\d{2})?$ // (3)!
^(10000|[1-9][0-9]{3,4})$ // (4)!
```

1. Range Validation from 0 to 100.
2. Positive number validation.
3. Decimal number Validation.
4. Minimum and maximum value validation between 1000 and 10 000.

##### URL validation

This validation is used to ensure that URLs provided by users for files or images adhere to the required format.

```js
(https:\/\/www\.|http:\/\/www\.|https:\/\/|http:\/\/)?[a-zA-Z0-9]{2,}(\.[a-zA-Z0-9]{2,})(\.[a-zA-Z0-9]{2,})?
```

#### Valid `boolean`

Allows you to define custom validation rules and error messages to guide users when their input doesn't meet required criteria.

For instance, you can use this property to validate a Create Password field, making sure it doesn't contain certain strings like `password` or `123`.

```js
{{ '{{
  !["password", "123", "admin"].some(subStr => {
    return Input1.text.toLowerCase().includes(subStr)
  })
}}' }}
```

#### Error Message `string`

Allows customization of the error message displayed when the user enters an incorrect value. By default, the input widget shows a generic `"invalid input"` message.

For example, if you want to add password validation, ensuring it is greater than 10 characters and contains at least one digit, you can use the following code in the **Error message** property.

```js

{{ '{{Input1.text.length > 10 && /\d/.test(Input1.text) ? true : false}}' }} // (1)!
{{ '{{Input1.text.length > 10 || !/\d/.test(Input1.text) ? "Error: Length should be at least 10 characters and contain at least one digit" : ""}}' }} // (2)!
```

1. Valid property.
2. Error message property.

This code checks the length of Input is exactly 10 characters and if it contains at least one digit. If not, it returns the error message

#### Min `number`

Sets a minimum value allowed for user input. Only appears when **Data Type** is set to Number.

#### Max `number`

Sets a maximum value allowed for user input. Only appears when **Data Type** is set to Number.

### General

#### Tooltip `string`

Enables you to add hints or provide additional information to guide the user regarding the required input.

#### Placeholder `string`

Allows you to set the placeholder text displayed within the input box. This can be used to provide a hint or example value to the user, guiding them on the expected format or content of the input.

#### Visible `boolean`

Controls the visibility of the widget. If you turn off this property, the widget would not be visible in View Mode. Additionally, you can use JavaScript by clicking on **JS** next to the **Visible** property to conditionally control the widget's visibility. The default value for the property is `true`.

For example, if you want to make the widget visible only when the user selects "Yes" from a Select widget, you can use the following JavaScript expression:

```js
{{ '{{Select1.selectedOptionValue === "Yes"}}' }}
```

#### Disabled `boolean`

Prevents users from selecting the widget. Even though the widget remains visible, user input is not permitted. Additionally, you can use JavaScript by clicking on **JS** next to the **Disabled** property to control the widget's disable state conditionally. The default value for the property is `false`.

For example, if you want to allow only a specific user to fill the input, you can use the following JavaScript expression:

```js
{{ '{{appsmith.user.email=="john@spread.ai"?false:true}}' }}
```

#### Animate Loading `boolean`

This property controls whether the widget is displayed with a loading animation. When enabled, the widget shows a skeletal animation during the loading process. Additionally, you can control it through JavaScript by clicking on the **JS** next to the property. The default value for the property is `true`.

#### Auto Focus `boolean`

When enabled, automatically places the user's cursor in the input box upon page load, directing their attention to the input field for immediate interaction.

#### Allow autofill `boolean`

When enabled, allows users to autofill input values using their web browser's saved data.

#### Height `string`

This property determines how the widget's height adjusts to changes in its content.

Options:

* **Fixed**: Maintains a constant height for the widget, allowing you to adjust it by dragging or using the resize handle.
* **Auto Height**: The widget's height adjusts dynamically in response to changes in its content.
* **Auto Height with limits**: Same as **Auto height**, with a configurable option to set the minimum and maximum number of rows the widget can occupy.

### Events

When the event is triggered, these event handlers can execute queries, JavaScript functions, or other [supported actions](../../reference/framework/global-functions.md).

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

### Icon

#### Icon `string`

Specifies the icon to be displayed on the widget. Additionally, you can use **JS** to dynamically set the icon. You can refer to the documentation of [blueprintjs](https://blueprintjs.com/docs/#icons) to explore a wide range of available icons.

### Label styles

#### Font color `string`

Represents the text color of the widget, specified as a [CSS color value](https://developer.mozilla.org/en-US/docs/Web/CSS/color). Additionally, the font color can be programmatically modified using JavaScript functions.

#### Font size `string`

Determines the font size of the label. It accepts [CSS font-size](https://developer.mozilla.org/en-US/docs/Web/CSS/font-size) values and can also be programmatically modified using JavaScript functions.

#### Emphasis `string`

Enables you to select a font style for the widget, such as bold or italic. Additionally, the font style can be programmatically modified using JavaScript functions.

### Border and shadow

#### Border radius `string`

Applies rounded corners to the outer edge of the widget. If JavaScript is enabled, you can specify valid [CSS border-radius](https://developer.mozilla.org/en-US/docs/Web/CSS/border-radius) to adjust the radius of the corners.

#### Box Shadow `string`

This property adds a drop shadow effect to the frame of the widget. If JavaScript is enabled, you can specify valid [CSS box-shadow](https://developer.mozilla.org/en-US/docs/Web/CSS/box-shadow) values to customize the appearance of the shadow.

## Reference properties

Reference properties are properties that are not available in the property pane but can be accessed using the dot operator in other widgets or JavaScript functions. They provide additional information or allow interaction with the widget programmatically. For instance, to get the visibility status, you can use `Input1.isVisible`.

#### text `string`

The `text` property retrieves the input value of the widget.

```js
{{ '{{Input1.text}}' }}
```

#### isValid `boolean`

The `isValid` property indicates the validation status of a widget, providing information on whether the widget's current value is considered valid or not.

```js
{{ '{{Input1.isValid}}' }}
```

#### isDisabled `boolean`

The `isDisabled` property reflects the state of the widget's **Disabled** setting. It is represented by a boolean value, where true indicates that the widget is not available, and false indicates that it is enabled for user interaction.

```js
{{ '{{Input1.isDisabled}}' }}
```

#### isVisible `boolean`

The `isVisible` property indicates the visibility state of a widget, with true indicating it is visible and false indicating it is hidden.

```js
{{ '{{Input1.isVisible}}' }}
```

## Methods

Widget property setters enable you to modify the values of widget properties at runtime, eliminating the need to manually update properties in the editor.

These methods are asynchronous and return a [Promise](../../writing-code-in-studio/using-js-promises.md). You can use the `.then()` block to ensure execution and sequencing of subsequent lines of code in Studio.

#### setVisibility (param: boolean): Promise

Sets the visibility of the widget.

```js
Input1.setVisibility(true)
```

#### setDisabled (param: boolean): Promise

Sets the disabled state of the widget.

```js
Input1.setDisabled(false)
```

#### setValue (param: string): Promise

Allows you to dynamically set the value of the widget.

```js
Input1.setValue("Hello123")
```

#### setRequired (param: boolean): Promise

Sets whether the widget is required or not.

```js
Input1.setRequired(true)
```
