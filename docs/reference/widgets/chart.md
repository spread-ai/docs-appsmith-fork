---
Title: Chart
Description: Chart widget reference
---

<!--
README

For guidance on how to write documenation, see https://dev.stage.spread.ai/docs/contributor/guide.html. Contact Documentation when this document is ready for review.
-->

This page provides information on how to use the Chart widget to visualize and represent data to create admin panels, dashboards, and other data-driven applications.

## Content properties

These properties are customizable options present in the property pane of the widget, allowing users to modify the widget according to their preferences.

### Data

#### Chart Type `string`

Allows you to choose from a variety of built-in chart types to visualize your data. Each chart type has its own unique way of representing data, allowing you to choose the most suitable visualization for your specific needs. Here are the available chart types:

* Line Chart
* Bar Chart
* Pie Chart
* Column Chart
* Area Chart
* Custom ECharts

#### Series title `string`

Sets the title of the current **Chart series**. This property is not available for Custom charts.

#### Series color `string`

Sets the color of the current **Chart series**. This property is not available for Custom charts.

#### Series data `array<object>`

Allows you to display data in the built-in charts, provide the data in the following structure:

Expected data structure:

```js
[
     {
          "x": "Product1",
          "y": 20000
     },..
]
```

In this format, **`x`** denotes the **label**, and **`y`** denotes the **value**. Additionally, you can display dynamic data from queries or JavaScript functions by binding the response to the **Series Data** property. For example, if you have a query named `fetchData`, you can bind its response using:

```js
{{ '{{fetchData.data}}' }}
```

If the query data is not in the expected format, you can use the `map()` function to transform it before passing it to the widget:

```js
{{ '{{fetchUserData.data.map( p => ({x: p.gender, y: p.count}))}}' }}
```

If the query fails and there is no default data specified, the chart doesn't render and appears empty.


#### Add Series `string`

Allows you to add multiple chart series. With this you can populate the chart with different sets of data and customize various aspects of its appearance, such as colors and labels.

### Custom EChart Configuration

[ECharts](https://echarts.apache.org/handbook/en/get-started/) is a JavaScript chart library by Apache that provides a wide range of chart types.

To display an ECharts in Studio, you can integrate it by embedding the ECharts code using mustache syntax, `{{ '{{<your-chart-data>}}' }}` in the **Custom EChart Configuration** property:

Expected data structure:

```js title="Basic line chart format"
{
     xAxis: {
          type: 'category',
          data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']
     },
     yAxis: {
          
     },
     series: [
          {
               data: [150, 230, 224, 218, 135, 147, 260],
               type: 'line'
          }
     ]
}
```

Graph information:

* **xAxis** specifies the type of data on the x-axis. For instance, you can use `category` as the `type` and provide an array of labeled values in the `data` field. The [xAxis](https://echarts.apache.org/handbook/en/concepts/axis) field is limited to specific chart types.

* **yAxis** specifies the type of data on the y-axis. For instance, to display values on the y-axis, you can set the `type` as `value`. The yAxis field is limited to specific chart types.

* **series** defines the [data points](https://echarts.apache.org/en/option.html#dataset) and the type of chart:
     * **type**: You can specify the type of chart you want to display, such as `line` for a line chart or `bar` for a bar chart.
     * **data**: Contains an array of values or categories, depending on the chart type. Alternatively, you can dynamically update the data using mustache syntax, like `{{ '{{Query1.data}}' }}`, enabling real-time data integration from external sources or queries, provided the data format aligns with the chart type's requirements.

### General

#### Title `string`

Sets the text that appears at the top of the chart as a title.

#### Visible `boolean`

Controls the visibility of the widget. If you turn off this property, the widget would not be visible in View Mode. Additionally, you can use JavaScript by clicking on **JS** next to the **Visible** property to conditionally control the widget's visibility.

For example, if you want to make the widget visible only when the user selects "Yes" from a Select widget, you can use the following JavaScript expression:

```js
{{ '{{Select1.selectedOptionValue === "Yes"}}' }}
```

#### Animate Loading `boolean`

This property controls whether the widget is displayed with a loading animation. When enabled, the widget shows a skeletal animation during the loading process. Additionally, you can control it through JavaScript by clicking on the **JS** next to the property.

### Axis

#### Adaptive Axis `boolean`

Determines the scaling behavior of the y-axis.

* OFF: The y-axis begins at zero and spans to an upper limit based on the data points;
* ON: The y-axis starting and ending values are both determined based upon the data points.

### Events

#### onDataPointClick

Specifies an [action](/reference/framework/global-functions.md) to be performed when a user clicks on a data point in the chart.

## Style properties

Style properties allow you to change the look and feel of the widget.

### Border and shadow

#### Border radius `string`

Applies rounded corners to the outer edge of the widget. If JavaScript is enabled, you can specify valid [CSS border-radius](https://developer.mozilla.org/en-US/docs/Web/CSS/border-radius) to adjust the radius of the corners.

#### Box Shadow `string`

This property adds a drop shadow effect to the frame of the widget. If JavaScript is enabled, you can specify valid [CSS box-shadow](https://developer.mozilla.org/en-US/docs/Web/CSS/box-shadow) values to customize the appearance of the shadow.

## Reference properties

Reference properties are properties that are not available in the property pane but can be accessed using the dot operator in other widgets or JavaScript functions. They provide additional information or allow interaction with the widget programmatically. For instance, to get the visibility status, you can use `Chart1.isVisible`.

#### xAxisName `string`

Contains the text of the x-axis Label setting of the chart.

```js
{{ '{{Chart1.xAxisName}}' }}
```

#### yAxisName `string`

Contains the text of the y-axis Label setting of the chart.

```js
{{ '{{Chart1.yAxisName}}' }}
```

#### chartData `array<object>`

Displays all the data related to the chart.

```js
{{ '{{Chart1.chartData}}' }}
```

#### selectedDataPoint `object: x, y, seriesTitle`

Contains an object which represents the data point that the user has most recently clicked `(object containing: x, y, seriesTitle)`.

```js
{{ '{{Chart1.selectedDataPoint}}' }} // (1)!
{{ '{{Chart1.selectedDataPoint.x}}' }} // (2)!
{{ '{{Chart1.selectedDataPoint.y}}' }} // (3)!
```

#### isVisible `boolean`

Reflects whether the widget is visible or not.

```js
{{ '{{Chart1.isVisible}}' }}
```

1. To access all the details of the selected data point.
2. To access the label of the selected data point.
3. To access the value of the selected data point.