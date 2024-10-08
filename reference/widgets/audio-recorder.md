---
Title: Audio Recorder
Description: Audio Recorder widget reference
---

<!--
README

For guidance on how to write documenation, see https://dev.stage.spread.ai/docs/contributor/guide.html. Contact Documentation when this document is ready for review.
-->

This page provides information on how to use the Audio Recorder widget to record audio using your microphone. The recorded audio is saved in WAV format.

## Content properties

These properties are customizable options present in the property pane of the widget, allowing users to modify the widget according to their preferences.

### General

#### Visible `boolean`

Controls the visibility of the widget. If you turn off this property, the widget is not visible in View mode. Additionally, you can use JavaScript by clicking on **JS** next to the **Visible** property to control the widget's visibility conditionally.

For example, if you want to make the widget visible only when the user checks an item in a Checkbox widget, you can use the following JavaScript expression in the visible property of the Audio Recorder widget:

```js
{{ '{{Checkbox1.isChecked}}' }}
```

#### Disabled `boolean`

Prevents users from selecting the widget. Even though the widget remains visible, user input is not permitted. Additionally, you can use JavaScript by clicking on **JS** next to the `Disabled` property to control the widget's disabled state conditionally.

For example, if you want to allow only a specific user to interact with the Audio Recorder widget, you can use the following JavaScript expression in the disabled property:

```js
{{ '{{appsmith.user.email=="john@spread.ai"?false:true}}' }}
```

#### Animate Loading `boolean`

Controls whether the widget is displayed with a loading animation. When enabled, the widget shows a skeletal animation during the loading process. Additionally, you can control it through JavaScript by clicking on the **JS** next to the property.

### Events

#### onRecordingStart

Allows you to configure one or multiple actions (Framework functions, queries, or JavaScript functions) to be executed when the recording starts.

#### onRecordingComplete

Allows you to configure one or multiple actions (Framework functions, queries, or JavaScript functions) to be executed when the recording ends.

## Style properties

Style properties allow you to change the look and feel of the widget.

### Styles

#### Icon color `string`

Sets the color of the mic icon in the Audio Recorder. If JavaScript is enabled, you can specify valid CSS-syntax [`color`](https://developer.mozilla.org/en-US/docs/Web/CSS/color) values to set the color of the icon.

#### Button color `string`

Sets the color of the widget's button. If JavaScript is enabled, you can specify valid CSS-syntax [`color`](https://developer.mozilla.org/en-US/docs/Web/CSS/color) values to set the color of the button.

### Border and shadow

#### Border radius `string`

Applies rounded corners to the outer edge of the widget. If JavaScript is enabled, you can specify valid [CSS border-radius](https://developer.mozilla.org/en-US/docs/Web/CSS/border-radius) to adjust the radius of the corners.

#### Box Shadow `string`

This property adds a drop shadow effect to the frame of the widget. If JavaScript is enabled, you can specify valid [CSS box-shadow](https://developer.mozilla.org/en-US/docs/Web/CSS/box-shadow) values to customize the appearance of the shadow.

## Reference properties

Reference properties enable you to access the widget's data and state using the dot operator in other widgets or JavaScript functions. They provide additional information or allow interaction with the widget programmatically. For instance, to retrieve the visibility status of a Select widget, you can use `AudioRecorder1.isVisible`.

#### blobURL `string`

Returns a binary URL that stores the audio for future use.

```js
{{ '{{AudioRecorder1.blobURL}}' }}
```

#### dataURL `string`

Stores the recorded audio in Data URL format (Base64). You can use it to embed the audio inline within different applications.

```js
{{ '{{AudioRecorder1.dataURL}}' }}
```

#### rawBinary `string`

Returns the audio file in binary format, suitable for storing the audio for future use.

```js
{{ '{{AudioRecorder1.rawBinary}}' }}
```

#### isVisible `boolean`

The `isVisible` property indicates the visibility state of a widget, with true indicating it is visible and false indicating it is hidden.

```js
{{ '{{AudioRecorder1.isVisible}}' }}
```

## Methods

Widget property setters enable you to modify the values of widget properties at runtime, eliminating the need to manually update properties in the editor.

These methods are asynchronous and return a [Promise](../../writing-code-in-studio/using-js-promises.md). You can use the `.then()` block to ensure the execution and sequencing of subsequent lines of code in Studio.

#### setVisibility (param: boolean): Promise

Sets the visibility of the Audio Recorder widget.

```js
AudioRecorder1.setVisibility(true)
```

#### setDisabled (param: boolean): Promise

Sets the disabled state of the widget.

```js
AudioRecorder1.setDisabled(false)
```

## Upload audio to S3

To upload recorded audio to Amazon S3:

1. Click the **+** icon next to the **queries/js** and choose your S3 datasource.
2. Select the method **Create a new file** from the Commands drop-down.
3. Provide the required parameters such as the bucket name and file type.
4. In the content body, add the following:

```js
{"data": {{ '{{AudioRecorder1.dataURL}}' }}}
```

4. Configure the **onRecordingComplete** event to run the query.

When recording is complete, the audio WAV file would be uploaded to the S3 Bucket.
