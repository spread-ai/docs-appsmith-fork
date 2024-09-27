---
description: Learn how to use the Switch Group widget which allows users to toggle multiple options.
---

# Switch Group

This page provides information on using the Switch Group widget, which allows users to toggle the on/off state for multiple options.

<VideoEmbed host="youtube" videoId="p--j-QyBlAY" title="How to use Switch Group Widget" caption="How to use Switch Group Widget"/>


## Content properties

These properties are customizable options present in the property pane of the widget, allowing users to modify the widget according to their preferences.


### Data


#### Options `array<object>`


 


This property allows you to set the labels and values for the options. Ensure that the values assigned to each option are unique. 

You can add these labels and values options in JSON format, like:


```js
[
 {
   "label": "Option1",
   "value": "OPTION1"
 },
 {
   "label": "Option2",
   "value": "OPTION2"
 }..
]
```
Additionally, you can dynamically display data from a query using JavaScript. For instance, you can use the `.map()` function to transform the data to the desired format, like:


```js
{{ '{{getCountry.data.map( p => ({label: p.country, value: p.country}))}}' }}
```





#### Default Selected Values `string`

 

Allows you to set default options in a widget. These options are initially selected when the widget is loaded, representing the user's default input unless modified. Multiple default options can be added by providing them as an array of values. 



```js
[
 "OPTION1", "OPTION2"
]
```





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


 
This validation feature allows you to designate the Switch Group as a mandatory field. For instance, when the widget is placed within a Form widget, enabling the Required property ensures that the Form's submit button remains disabled until the Switch Group is turned on/off.







### General


#### Tooltip `string`
 


This feature enables you to add hints or provide additional information to guide the user regarding the required input.



#### Visible `boolean`

 

This property controls the visibility of the widget. If you turn off this property, the widget would not be visible in view mode. Additionally, you can use JavaScript by clicking on `JS` next to the **Visible** property to conditionally control the widget's visibility. 



#### Disabled `boolean`

 

This property prevents users from selecting the widget. Even though the widget remains visible, user input is not permitted. Additionally, you can use JavaScript by clicking on `JS` next to the **Disabled** property to control the widget's disable state conditionally.



#### Inline `boolean`

 

When the inline property is enabled, the options are displayed horizontally within the widget. When this property is turned off, the options are displayed in a vertical format.




#### Animate Loading `boolean`


 

This property controls whether the widget is displayed with a loading animation. When enabled, the widget shows a skeletal animation during the loading process. Additionally, you can control it through JavaScript by clicking on the <code>JS</code> next to the property.




#### Height `string`


 
This property determines how the widget's height adjusts to changes in its content. There are three available options:


* **Fixed**: The widget's height remains as set using drag and resize.
* **Auto Height**: The widget's height adjusts dynamically in response to changes in its content.
* **Auto Height with limits**: Same as **Auto height**, with a configurable option to set the minimum and maximum number of rows the widget can occupy.





### Events


#### onSelectionChange

 

This event defines the action that would be executed when the user selects or deselects multiple or single options in the switch group. It allows you to specify a list of [actions](/reference/framework/global-functions.md) that can be triggered in response to the switch state change.





## Style properties
Style properties allow you to change the look and feel of the widget.

#### Font color `string`

 

Represents the text color of the widget, specified as a [CSS color value](https://developer.mozilla.org/en-US/docs/Web/CSS/color).  It can also be manipulated programmatically using the JavaScript functions.



#### Font size `string`

 

Determines the font size of the label. It accepts [CSS font-size](https://developer.mozilla.org/en-US/docs/Web/CSS/font-size) values and can also be programmatically modified using JavaScript functions.



#### Emphasis `string`

 

Enables you to select a font style for the widget, such as bold or italic. Additionally, the font style can be programmatically modified using JavaScript functions.



### General

#### Alignment 

 

It allows you to specify how the label should be positioned relative to the switch.



### Color

#### Accent color `string`

 

Defines the accent color of the widget, which is used as the fill color for the switch when it is turned on. It accepts [CSS color values](https://developer.mozilla.org/en-US/docs/Web/CSS/color) and can also be programmatically modified using JavaScript functions.




## Reference properties
These properties are not available in the property pane, but can be accessed using the dot operator in other widgets or JavaScript functions. For instance, to get the visibility status, you can use `SwitchGroup1.isVisible`.


#### selectedValues `array`

 

The `selectedValues` property holds an array of values that represents the options selected by the user.



```js
{{ '{{SwitchGroup1.selectedValues}}' }}
```







## Methods

Widget property setters enable you to modify the values of widget properties at runtime, eliminating the need to manually update properties in the editor.

These methods are asynchronous and return a [Promise](/writing-code-in-studio/using-js-promises.md). You can use the `.then()` block to ensure execution and sequencing of subsequent lines of code in Appsmith.



#### setVisibility (param: boolean): Promise

 

Sets the visibility of the widget.



```js
SwitchGroup1.setVisibility(true)
```





#### setDisabled (param: boolean): Promise

 

Sets the disabled state of the widget.



```js
SwitchGroup1.setDisabled(false)
```




#### setRequired (param: boolean): Promise

 

Sets whether the widget is required or not.



```js
SwitchGroup1.setRequired(true)
```



