---
Title: Datepicker
Description: Datepicker widget reference
---

<!--
README

For guidance on how to write documenation, see https://dev.stage.spread.ai/docs/contributor/guide.html. Contact Documentation when this document is ready for review.
-->

This page describes the properties of the Datepicker widget which can be used to display or capture date/time information. It enables to filter the data based on a date range, format dates and performs date validations.

## Content properties

These properties are customizable options present in the property pane of the widget, allowing users to modify the widget according to their preferences.

### Data

#### Date format `ISO 8601 date string`

Displays a list of date formats for the Datepicker widget. With **JS** enabled, this property accepts [ISO 8601 date string](https://www.iso.org/iso-8601-date-and-time-format.html) formats.

You can also use the built-in [**Moment.js**](https://momentjs.com/docs/) library in Studio to parse the date in the format required.

For example, if you want to convert the selected date and time to the IST timezone (Asia/Kolkata), click the **JS** button and add the following code:

```js
{{ '{{ moment(datePickerName.selectedDate).tz("Asia/Kolkata").format() }}' }}
```

#### Default date `ISO 8601 date string`

Sets a default date that would be captured as user input unless it is changed by the user. With **JS** enabled, this property accepts [ISO 8601 date string](https://www.iso.org/iso-8601-date-and-time-format.html) values.

#### First day of the week `number`

Sets which day of the week appears first within the calendar of the Datepicker's menu.

#### Time precision `string`

Decides whether a time is included within the Datepicker, and whether that time is to the minute or second precision. With **JS** enabled, it accepts the following values - `None`, `minute`, or `second`.

### Label

#### Text `string`

Sets the label text displayed in the Datepicker widget.

### Validation

#### Required

Enables you to designate the Datepicker widget as a mandatory field.

#### Min date `ISO 8601 date string`

Sets a minimum date permitted to be selected in the widget. With **JS** enabled, this property accepts [ISO 8601 date string](https://www.iso.org/iso-8601-date-and-time-format.html) values.

#### Max date `ISO 8601 date string`

Sets a maximum date permitted to be selected with the widget. With **JS** enabled, this property accepts [ISO 8601 date string](https://www.iso.org/iso-8601-date-and-time-format.html) values.

### General

#### Tooltip

Sets a tooltip that appears when the user hovers over the widget. It enables you to add hints or provide additional information for the widget. Additionally, you can control it through JavaScript by clicking on the **JS** next to the property.

#### Visible `boolean`

Controls the visibility of the widget. If you turn off this property, the widget is not visible in View mode. Additionally, you can use JavaScript by clicking on **JS** next to the **Visible** property to control the widget's visibility conditionally.

For example, if you want to make the widget visible only when the user checks an item in a Checkbox widget, you can use the following JavaScript expression in the visible property of the Datepicker widget:

```js
{{ '{{Checkbox1.isChecked}}' }}
```

#### Disabled `boolean`

Prevents users from selecting the widget. Even though the widget remains visible, user input is not permitted. Additionally, you can use JavaScript by clicking on **JS** next to the **Disabled** property to control the widget's disabled state conditionally.

For example, if you want to allow only a specific user to interact with the Datepicker widget, you can use the following JavaScript expression:

```js
{{ '{{appsmith.user.email=="john@spread.ai"?false:true}}' }}
```

#### Animate Loading `boolean`

Controls whether the widget is displayed with a loading animation. When enabled, the widget shows a skeletal animation during the loading process. Additionally, you can control it through JavaScript by clicking on the **JS** next to the property.

#### Show shortcuts `boolean`

When enabled, it adds section within the Datepicker pop-up that contains options - **Today**, **1 week ago**, **1 month ago**,**3 months ago**, **1 year ago**, for quick date selection.

#### Close on selection `boolean`

Sets whether the Datepicker menu should automatically close upon user selection of a date.

#### Height `string`

This property determines how the widget's height adjusts to changes in its content. There are three available options:

- **Fixed:** The height of the widget remains as set using drag and resize.
- **Auto Height:** The widget's height adjusts dynamically in response to changes in its content.
- **Auto Height with limits:** Same as Auto height, with a configurable option to set the minimum and maximum number of rows the widget can occupy.

### Events

When an event is triggered, these event handlers can execute queries, JavaScript code, or other supported [actions](/reference/framework/global-functions.md).

#### onDateSelected

Triggered when the user selects a date in the Datepicker widget.  

#### onFocus

Triggered when the widget gets focus, when user clicks on the widget.

#### onBlur

Triggered when the widget loses focus, when the user clicks outside of the widget or interacts with another entity on the page.

## Style properties

Style properties allow you to change the look and feel of the widget.

### Label styles

#### Font color `string`

Enables you to set text color for the label. Additionally, click the **JS** button to programmatically modify the text color using JavaScript functions.

#### Font size `string`

Enables you to control the size of the label text. Additionally, click the **JS** button to programmatically modify text size using JavaScript functions.

#### Emphasis `string`

Enables you to choose a font style; bold or italic. Additionally, click the **JS** button to programmatically modify the font style using JavaScript functions.

### Border and shadow

#### Border radius `string`

Applies rounded corners to the outer edge of the widget. If JavaScript is enabled, you can specify valid [CSS border-radius](https://developer.mozilla.org/en-US/docs/Web/CSS/border-radius) to adjust the radius of the corners.

#### Box Shadow `string`

This property adds a drop shadow effect to the frame of the widget. If JavaScript is enabled, you can specify valid [CSS box-shadow](https://developer.mozilla.org/en-US/docs/Web/CSS/box-shadow) values to customize the appearance of the shadow.

## Reference properties

Reference properties enable you to access the widget's data and state using the dot operator in other widgets or JavaScript functions. They provide additional information or allow interaction with the widget programmatically. For instance, to retrieve the visibility status of a Datepicker widget, you can use `Datepicker1.isVisible`.

#### formattedDate `string`

Contains the formatted date value currently selected within the Datepicker widget. This value changes if the default value is updated or the user inputs a new value. The format depends on the **Date Format** property set for the widget.

```js
{{ '{{Datepicker1.formattedDate}}' }}
```

#### selectedDate `string`

Contains the ISO date string value selected in the Datepicker widget. This value changes if the default value is updated or the user inputs a new value.

```js
{{ '{{Datepicker1.selectedDate}}' }}
```

#### isDisabled `boolean`

It reflects the state of the widget's Disabled setting. It is represented by a boolean value, where `true` indicates that the widget is disabled, and `false` indicates that it is enabled for user interaction.

```js
{{ '{{Datepicker1.isDisabled}}' }}
```

#### isVisible `boolean`

The `isVisible` property indicates the visibility state of a widget, with true indicating it is visible and false indicating it is hidden.

```js
{{ '{{Datepicker1.isVisible}}' }}
```

## Methods

Widget property setters enable you to modify the values of widget properties at runtime, eliminating the need to manually update properties in the editor.

These methods are asynchronous and return a [Promise](/writing-code-in-studio/using-js-promises.md). You can use the `.then()` block to ensure execution and sequencing of subsequent lines of code in Studio.

#### setVisibility (param: boolean): Promise

Sets the visibility of the widget.

```js
DatePicker1.setVisibility(true)
```

#### setDisabled (param: boolean): Promise

Sets the disabled state of the widget.

```js
DatePicker1.setDisabled(false)
```

#### setValue (param: string): Promise

Allows you to dynamically set the value of the widget.

```js
DatePicker1.setValue('11-01-1994')
```

#### setRequired (param: boolean): Promise

Sets whether the widget is required or not.

```js
DatePicker1.setRequired(true)
```
