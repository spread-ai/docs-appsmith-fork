---
description: Learn how to use the Progress widget to visually track the progress of tasks or processes in your application.
---
# Progress

This page provides information on using the Progress widget, which is used to visualize the progression of specific operations and user or system-triggered actions.



<VideoEmbed host="youtube" videoId="Yg1Pfy7uc1s" title="How to use Progress Widget" caption="How to use Progress Widget"/>

## Content properties


These properties are customizable options present in the property pane of the widget, allowing users to modify the widget according to their preferences.


### Basic

#### Infinite loading `boolean`

 

Enables the widget to enter an infinite loading state, which is beneficial when the progress values cannot be determined. For instance, this property can be enabled for queries that take a longer time to execute.



#### Type `string`

 

Allows you to select the desired format for the progress bar.

Options:
* Circular
* Linear




#### Progress `number`

 

Specify the value of the progress indicator (in percentage). You can also use values retrieved from queries or JavaScript functions within the mustache operator `{{ '{{}}' }}`.




### General

#### Number of steps `number`

 

Specify the number of steps to break down the progress bar into multiple parts with fixed progress percentages. This property only supports positive integers.




#### Visible `boolean`

 

Controls the visibility of the widget. If you turn off this property, the widget would not be visible in View Mode. Additionally, you can use JavaScript by clicking on **JS** next to the **Visible** property to conditionally control the widget's visibility.

For example, if you want to make the widget visible only when the user selects "Yes" from a Select widget, you can use the following JavaScript expression: 
```js
{{ '{{Select1.selectedOptionValue === "Yes"}}' }}
```



#### Show result `boolean`

 

Control the display of the evaluated percentage as a number along with the progress in the widget.




#### Counterclockwise  `boolean`

 

Specifies whether the circular progress bar should animate in a counterclockwise direction. This option is only available when the Circular progress **Type** is selected.




## Style properties
Style properties allow you to change the look and feel of the widget.

#### Fill color `string`

 

Specify the color of the progress bar. It accepts [CSS color values](https://developer.mozilla.org/en-US/docs/Web/CSS/color) and can also be programmatically modified using JavaScript functions.




## Reference properties

These properties are not available in the property pane, but can be accessed using the dot operator in other widgets or JavaScript functions. For instance, to get the visibility status, you can use `Progress1.isVisible`.

#### progress `number`

 

Indicates the current progress of the progress bar as a percentage.



```js
{{ '{{Progress1.progress}}' }}
```




#### isVisible `boolean`
 

The `isVisible` property indicates the visibility state of a widget, with true indicating it is visible and false indicating it is hidden.



```js
{{ '{{Progress1.isVisible}}' }}
```




## Methods

The methods provided by the widget allow users to dynamically update and manipulate its properties, facilitating the creation of dynamic and interactive applications without the need for manual property modifications. 

These methods are asynchronous and return a [Promise](/writing-code-in-studio/using-js-promises.md). You can use the `.then()` block to ensure execution and sequencing of subsequent lines of code in Studio.



#### setVisibility (param: boolean): Promise

 

Sets the visibility of the widget.



```js
Progress1.setVisibility(true)
```




#### setProgress (param: number): Promise

 

Sets the progress value of the Progress widget.



```js
Progress1.setProgress(50)
```

