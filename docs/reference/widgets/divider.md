---
Description: The Divider widget is used to visually separate or compartmentalise different parts of your application.
---
# Divider

This page provides information on using the Divider widget, which serves the purpose of visually separating or compartmentalizing various sections within your application.

## Content properties

These properties are customizable options present in the property pane of the widget, allowing users to modify the widget according to their preferences.


### General

#### Visible `boolean`

 

Controls the visibility of the widget. If you turn off this property, the widget would not be visible in View Mode. Additionally, you can use JavaScript by clicking on **JS** next to the **Visible** property to conditionally control the widget's visibility. Default value is set to `true`.

For example, if you want to make the widget visible only when the user selects "Yes" from a Select widget, you can use the following JavaScript expression: 
```js
{{ '{{Select1.selectedOptionValue === "Yes"}}' }}
```





#### Animate Loading `boolean`


 

This property controls whether the widget is displayed with a loading animation. When enabled, the widget shows a skeletal animation during the loading process. Additionally, you can control it through JavaScript by clicking on the **JS** next to the property. Default value is set to `true`.



## Style properties

Style properties allow you to change the look and feel of the widget.

### General

#### Direction `string` 

 

Determines the orientation of the widget's line, allowing you to choose between horizontal and vertical alignments. When JavaScript is enabled, accepted values are `horizontal` or `vertical`.



### Stroke

#### Color `string`

 

Specify the color of the divider. It accepts [CSS color values](https://developer.mozilla.org/en-US/docs/Web/CSS/color) and can also be programmatically modified using JavaScript functions.




#### Style `string`

 

Sets the type of line used for the divider.

Options:
* Solid: A continuous and unbroken line.
* Dashed: A line composed of short, evenly spaced dashes.
* Dotted: A line made up of small, distinct dots.

With JS is enabled, accepts strings with value `solid`, `dashed`, or `dotted`.




#### Thickness `number` 


 

Sets the thickness of the divider line in pixels. 



### Cap

#### Cap `string`

 

Sets the design of the cap to be added to the end of the divider line.

Options:
* No Cap
* Arrow
* Dot



#### Cap position `string`

 

Determines the placement of caps on the sides of the divider line. 

Options:

* Left
* Both
* Right



## Reference properties

These properties are not available in the property pane, but can be accessed using the dot operator in other widgets or JavaScript functions. For instance, to get the visibility status, you can use `Divider1.isVisible`.

#### capType `string`

 

Indicates the widget's Cap style property, shows whether the divider line is capped with a Dot, an Arrow, or No cap. 




```js
{{ '{{Divider1.capType}}' }}
```





#### capSide `number`

 

Reflects the widget's Cap Position style property, indicating the sides of the divider line where caps are located. Numeric values include:

* `-1` for the left or top side only
* `0` for both sides
* `1` for the right or bottom side only



```js
{{ '{{Divider1.capSide}}' }}
```




#### dividerColor `string`

 

Reflects the color value of the divider line, presented in the form of a hexadecimal color code.




```js
{{ '{{Divider1.dividerColor}}' }}
```





#### orientation `string`

 

Reflects the **Orientation** of the widget, values are strings either `horizontal` or `vertical`.




```js
{{ '{{Divider1.orientation}}' }}
```




#### strokeStyle `string`

 

Reflects the widget's **Dash Style** property as a string with value either `solid`, `dashed`, or `dotted`.




```js
{{ '{{Divider1.strokeStyle}}' }}
```





#### thickness `number`

 

Reflects the thickness of the divider line as a number of pixels.




```js
{{ '{{Divider1.thickness}}' }}
```




#### isVisible `boolean`

 

The `isVisible` property indicates the visibility state of a widget, with true indicating it is visible and false indicating it is hidden.



```js
{{ '{{Divider1.isVisible}}' }}
```



## Methods

Widget property setters enable you to modify the values of widget properties at runtime, eliminating the need to manually update properties in the editor.

These methods are asynchronous and return a [Promise](/writing-code-in-studio/using-js-promises.md). You can use the `.then()` block to ensure execution and sequencing of subsequent lines of code in Appsmith.


#### setVisibility (param: boolean): Promise

 

Sets the visibility of the widget.



```js
Divider1.setVisibility(true)
```

