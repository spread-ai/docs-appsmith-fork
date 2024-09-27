---
description: >-
  MultiSelect widget reference
---

# MultiSelect

This page explains how to use a MultiSelect widget to allow users to select multiple options from a given list.


## Content properties

These properties are customizable options present in the property pane of the widget, allowing users to modify the widget according to their preferences.

### Data

#### Source Data `array<object>`

 

Specify data as an array of objects to display options in the widget. For example:


```js
[
  {
    name: "Blue",
    code: "BLUE"
  },
  {
    name: "Green",
    code: "GREEN"
  },
  {
    name: "Red",
    code: "RED"
  },
];
```

You can dynamically generate options by fetching data from queries or JavaScript functions and binding the response to the **Source Data** property. For example, if you have a query named `fetchData`, you can bind its response using:

```js
{{ '{{fetchData.data}}' }}
```

If the retrieved data is not in the desired format, you can use JavaScript to transform the data by adding it to the **Source Data** property:

```js
{{ '{{fetchData.data.map( p => ({label: p.country, value: p.country}))}}' }}
```


If you are generating options for MutliSelect widget using JS code as shown above, you must define both the [**Label**](#label-string) and [**Value**](#value-string) properties.



#### Label `string`

 

Defines the key from the **Source Data** property that specifies the labels for each option in the MultiSelect widget. To define **Label** using code, click the **JS** button next to the property. 

For example, If you prefer the label to be displayed in lowercase, you can achieve this using the following code snippet:

```js
{{ '{{ item.name.toLowerCase() }}' }}
```
`item.name` represents the Source Data's property containing the label, and the `toLowerCase()` function is applied to convert the label to lowercase.



#### Value `string`

 

Defines the key from the **Source Data** property that specifies the values for each option in the MultiSelect widget. Value defined for each option must be unique. To define **Value** using code, click the **JS** button next to the property.




#### Default selected value `string`

 

Sets the initial options that are automatically chosen when the widget is loaded. It serves as the default selection unless the user manually selects another option from the list. Multiple values can be provided in a CSV format or an array of strings for a MultiSelect dropdown. For example, if you want the default option to be `Blue` and `Red`, set the **Default Selected Value** property to:

```js
[
  "GREEN",
  "RED"
]
```




### Label

#### Text `string`

 

Sets the label of the widget.



#### Position `string`

 

Sets the placement of the **Label** in the widget.

Options:
- **Left**: The label is placed on the left of the widget.
- **Top**: The label gets placed at the top of the widget.
- **Auto**: The label position is determined based on the height of the widget itself. 



#### Alignment `string`

 

Sets the label alignment of the widget when the position selected is **Left**.



#### Width (in columns) `number`

 

Sets the width of the label in the widget when the **Left** position is selected.



### Search and filters

#### Allow searching `boolean`

 

Enables searching for options within the dropdown list. When this option is enabled, a search input field is displayed in the widget. Additionally, you can control it through JavaScript by clicking on the **JS** next to the property.



#### Server side filtering `boolean`

 

Enables server-side filtering via a query request. Use this property when the MultiSelect widget's option data is being bound to a query.



#### onFilterUpdate

 

This event allows you to configure one or multiple actions (Framework functions, queries, or JavaScript functions) to be executed when you update the filter text. You can also write custom JavaScript logic for this event by clicking on the **JS** next to the property.




### Validations

#### Required `boolean`

 

Enabling this property for a MultiSelect widget makes it a mandatory field, meaning that the user must select a value from the dropdown. When the MultiSelect widget is placed within a Form widget and the **Required** property is enabled, the Form's submit button remains inactive until a value is selected in the MultiSelect widget.



### General 

#### Tooltip `string`

 

Sets a tooltip for the widget. You can add hints or extra information about the required input from the user



#### Placeholder `string`

 

Sets the placeholder text for the MultiSelect widget. 



#### Visible `boolean`

 

Controls the visibility of the widget. If you turn off this property, the widget is not visible in View mode. Additionally, you can use JavaScript by clicking on **JS** next to the **Visible** property to control the widget's visibility conditionally.

For example,  if you want to make the widget visible only when the user checks an item in a Checkbox widget, you can use the following JavaScript expression in the visible property of the MultiSelect widget:

```js
{{ '{{Checkbox1.isChecked}}' }}
```



#### Disabled `boolean`

 

Prevents users from selecting the widget. Even though the widget remains visible, user input is not permitted. Additionally, you can use JavaScript by clicking on **JS** next to the `Disabled` property to control the widget's disabled state conditionally.

For example, if you want to allow only a specific user to interact with the Multi+-select widget, you can use the following JavaScript expression: 
```js
{{ '{{appsmith.user.email=="john@spread.ai"?false:true}}' }}
```




#### Animate Loading `boolean`

 

Controls whether the widget is displayed with a loading animation. When enabled, the widget shows a skeletal animation during the loading process. Additionally, you can control it through JavaScript by clicking on the **JS** next to the property.



#### Allow select all `boolean`

 

Controls the visibility of **Select all** option in the dropdown. When enabled, **Select all** option is visible at the top of the dropdown, allowing you to select all the options with one click.



#### Height `string`

 

This property determines how the widget's height adjusts to changes in its content. 

Options:

- **Fixed:** The height of the widget remains as set using drag and resize.
- **Auto Height:** The widget's height adjusts dynamically in response to changes in its content.
- **Auto Height with limits:** Same as Auto height, with a configurable option to set the minimum and maximum number of rows the widget can occupy.



### Events

#### onOptionChange 

 

Allows you to configure one or multiple actions (Framework functions, queries, or JavaScript functions) to be executed when the user selects an option in the dropdown list. It enables you to capture the user's input and perform specific actions in response. You can also write custom JavaScript logic for this event by clicking on the **JS** button next to the property.



#### onDropdownOpen

 

Allows you to configure one or multiple actions (Framework functions, queries, or JavaScript functions) to be executed when the user opens the dropdown list. For example, you could use the **onDropdownOpen** event to retrieve data from a database, populate the options in the dropdown list, or display additional information to the user. You can also write custom JavaScript logic for this event by clicking on the **JS** button next to the property.




#### onDropdownClose 

 

Allows you to configure one or multiple actions (Framework functions, queries, or JavaScript functions) to be executed when the user closes the dropdown list. For example, you could use the **onDropdownClose** event to store the selected option in a database, hide additional information, or reset the widget to its original state. You can also write custom JavaScript logic for this event by clicking on the **JS** button next to the property.



## Style properties

Style properties allow you to change the look and feel of the widget.

### Label styles

#### Font color `string`

 

Allows you to set text color for the label. Additionally, you can programmatically modify the text color using JavaScript functions.



#### Font size `string`

 

Allows you to control the size of the label text. Additionally, you can programmatically modify the text size using JavaScript functions.



#### Emphasis `string`

 

Allows you to choose a font style; bold or italic. You can click on the **JS** button to programmatically modify the font style using JavaScript functions.



### Border and shadow

#### Border radius `string`

 

Applies rounded corners to the outer edge of the widget. To control the border radius programmatically, click the **JS** button to enable JavaScript and specify a valid [CSS border-radius](https://developer.mozilla.org/en-US/docs/Web/CSS/border-radius) to adjust the radius of the corners.



#### Box Shadow `string`
 

 

This property adds a drop shadow effect to the frame of the widget. To control the Box Shadow programmatically, click the **JS** button to enable JavaScript and specify a valid [CSS box-shadow](https://developer.mozilla.org/en-US/docs/Web/CSS/box-shadow) value to customize the appearance of the shadow.



## Reference properties

Reference properties enable you to access the widget's data and state using the dot operator in other widgets or JavaScript functions. They provide additional information or allow interaction with the widget programmatically. For instance, to retrieve the visibility status of a select widget, you can use `MultiSelect1.isVisible`.

#### filterText `string`

 

Returns the text entered in the search filter of the MultiSelect widget. For more information, see [Server side filtering](/reference/widgets/select#server-side-filtering).



```js
{{ '{{MultiSelect1.filterText}}' }}
```



#### isDisabled `boolean`

 

It reflects the state of the widget's Disabled setting. It is represented by a boolean value, where `true` indicates that the widget is disabled, and `false` indicates that it is enabled for user interaction.



```js
{{ '{{MultiSelect1.isDisabled}}' }}
```



#### isVisible `boolean`

 

The `isVisible` property indicates the visibility state of a widget, with true indicating it is visible and false indicating it is hidden.


```js
{{ '{{MultiSelect1.isVisible}}' }}
```



####  isDirty `boolean`

 

This property is a boolean value that indicates whether the user has interacted with the widget. If the user selects an option from the dropdown list, the `isDirty` property returns `true`. However, if the user does not make any selection and the initial value remains unchanged, the `isDirty` property returns `false`.



```js
{{ '{{MultiSelect1.isDirty}}' }}
```



#### options `array`

 

Returns an array of objects that contain the label and value of the options in the dropdown list.



```js
{{ '{{MultiSelect1.options}}' }}
```



#### selectedOptionValues `string`

 

Returns the value of the option displayed in the MultiSelect widget. It changes if the default value of the widget changes or the user selects an option.



```js
{{ '{{MultiSelect1.selectedOptionValues}}' }}
```



#### selectedOptionLabels `string`

 

Returns the label of the option displayed in the MultiSelect widget. It changes if the default value of the widget changes or the user selects an option.



```js
{{ '{{MultiSelect1.selectedOptionLabels}}' }}
```




## Methods

Widget property setters enable you to modify the values of widget properties at runtime, eliminating the need to manually update properties in the editor.

These methods are asynchronous and return a [Promise](/writing-code-in-studio/using-js-promises.md). You can use the `.then()` block to ensure execution and sequencing of subsequent lines of code in Studio.


#### setDisabled (param: boolean): Promise

 

Sets the `disabled` state of the widget.



```js
MultiSelect1.setDisabled(false)
```



#### setRequired (param: boolean): Promise

 

Sets whether the widget is required or not.



```js
MultiSelect1.setRequired(true)
```




#### setSelectedOptions (param: object): Promise

 

Sets the selected option of the MultiSelect widget.



```js
MultiSelect1.setSelectedOption({ label: 'Option 2', value: 'option2' })
```


