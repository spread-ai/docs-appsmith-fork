---
Title: Button
Description: Button widget reference
---

<!--
README

For guidance on how to write documenation, see https://dev.stage.spread.ai/docs/contributor/guide.html. Contact Documentation when this document is ready for review.
-->

This page provides information on the button widget, enabling you to trigger actions or perform specific tasks with a simple click.

## Content properties

These properties are customizable options present in the property pane of the widget, allowing users to modify the widget according to their preferences.

### Basic

#### Label `string`

Sets the text that appears on the button.

#### onClick

Allows you to configure one or multiple actions (Framework functions, queries, or JavaScript functions) to be executed when the button is clicked. You can chain multiple actions together, and all the nested actions would run simultaneously.

### General

#### Tooltip `string`

Sets a tooltip that appears when the user hovers over the widget. It enables you to add hints or provide additional information for the button.

#### Visible `boolean`

Controls the visibility of the widget. If you turn off this property, the widget is not visible in View mode. Additionally, you can use JavaScript by clicking on **JS** next to the **Visible** property to control the widget's visibility conditionally.

For example, if you want to make the button visible only when the user selects "Yes" from a Select widget, you can use the following JavaScript expression:

```js
{{ '{{Select1.selectedOptionValue === "Yes"}}' }}
```

#### Disabled `boolean`

Prevents users from selecting the widget. Even though the widget remains visible, user input is not permitted. Additionally, you can use JavaScript by clicking on **JS** next to the **Disabled** property to control the widget's `disabled` state conditionally.

For example, if you want to allow only a specific user to click the button, you can use the following JavaScript expression:

```js
{{ '{{appsmith.user.email=="john@spread.ai"?false:true}}' }}
```

#### Animate Loading `boolean`

Controls whether the widget is displayed with a loading animation. When enabled, the widget shows a skeletal animation during the loading process. Additionally, you can control it through JavaScript by clicking on the **JS** next to the property.

### Validation

#### Google reCAPTCHA key

Add a Google reCAPTCHA [site key](https://cloud.google.com/recaptcha-enterprise/docs/create-key) here to enable Google reCAPTCHA check to the button. The token is accessible from the API pane with the `recaptchaToken` key (see the [Google reCAPTCHA](https://www.google.com/recaptcha/about/) docs). For more information, see [Google reCAPTCHA](google-recaptcha.md).

#### Google reCAPTCHA version

Sets the Google reCAPTCHA version to use for the button, either v2 or v3.

### Form settings

Buttons can have some special behaviors when they're located within the boundaries of a [Form widget](form.md). Its form-specific behavior is controlled by two of the button's properties:

#### Disabled invalid forms

When this button property is turned on, the button remains disabled if the associated form contains any required fields that are incomplete or if any of the form fields contain input that is considered invalid.

For example, if you have a form with an Input widget whose **Required** property is turned on. If that input field hasn't been completed by the user, then the button won't be usable.

#### Reset form on success

When this button property is turned on, the button can be used to reset all fields present in the form's area to their default state. This is useful for clearing inputs after the form is submitted.

## Style properties

Style properties allow you to change the look and feel of the button.

### General

#### Button variant `string`

Specifies the style type of the button to indicate its significance.

Options:

* **Primary**: Fills the button with color.
* **Secondary**: Adds a colored border to the button while keeping the button itself white.
* **Tertiary**: This option does not apply any specific styling changes to the button.

This property can be dynamically set using JavaScript by providing a string value of `PRIMARY`, `SECONDARY`, or `TERTIARY`.

### Icon

#### Select icon `string`

Specifies the icon to be displayed on the button. Additionally, you can use **JS** to dynamically set the icon. You can refer to the documentation of [blueprintjs](https://blueprintjs.com/docs/#icons) to explore a wide range of available icons.

#### Position `string`

This property allows you to configure the **Icon**'s placement.

Options:

* **Left**: Aligns the icon to the left side of the Label.
* **Right**: Aligns the icon to the right side of the Label.

#### Placement `string`

Determines the spacing between the **Icon** and the **Label**.

Options:

* **Start**: The icon and label appear on the leftmost side of the button.
* **Between**: The icon and label appear at opposite ends of the button's space.
* **Center**: The icon and label appear in the center of the button space.

This property can be dynamically set using JavaScript by providing a string value of `START`, `CENTER`, or `BETWEEN`.

### Color

#### Button color `string`

Represents the color of the button, specified as a [CSS color value](https://developer.mozilla.org/en-US/docs/Web/CSS/color). Additionally, the font color can be programmatically modified using JavaScript functions.

### Border and shadow

#### Border radius `string`

Applies rounded corners to the outer edge of the widget. If JavaScript is enabled, you can specify a valid [CSS border-radius](https://developer.mozilla.org/en-US/docs/Web/CSS/border-radius) to adjust the radius of the corners.

#### Box Shadow `string`

This property adds a drop shadow effect to the frame of the widget. If JavaScript is enabled, you can specify valid [CSS box-shadow](https://developer.mozilla.org/en-US/docs/Web/CSS/box-shadow) values to customize the appearance of the shadow.

### Reference properties

Reference properties enable you to access the widget's data and state using the dot operator in other widgets or JavaScript functions. They provide additional information or allow interaction with the widget programmatically. For instance, to retrieve the visibility status of a  button widget, you can use `Button1.isVisible`.

#### text `string`

Returns the value of the button's label property.

```js
{{ '{{Button1.text}}' }}
```

#### isVisible `boolean`

Indicates the visibility state of a widget, with true indicating it is visible and false indicating it is hidden.

```js
{{ '{{Button1.isVisible}}' }}
```

#### isDisabled `boolean`

It reflects the state of the widget's **Disabled** setting. It is represented by a boolean value, where true indicates that the widget is disabled, and false indicates that it is enabled for user interaction.

```js
{{ '{{Button1.isDisabled}}' }}
```

## Methods

Widget property setters enable you to modify the values of widget properties at runtime, eliminating the need to manually update properties in the editor.

These methods are asynchronous and return a [Promise](../../writing-code-in-studio/using-js-promises.md). You can use the `.then()` block to ensure execution and sequencing of subsequent lines of code in Studio.

#### setVisibility (param: boolean): Promise

Sets the visibility of the widget.

```js
Button1..setVisibility(true)
```

#### setDisabled (param: boolean): Promise

Sets the `disabled` state of the widget.

```js
Button1.setDisabled(false)
```

#### setColor (param: string): Promise

Sets the background color of the button widget.

```js
Button1.setColor('#FF0000')
```

#### setLabel (param: string): Promise

Sets the label of the button widget.

```js
Button1.setLabel('Click me!')
```
