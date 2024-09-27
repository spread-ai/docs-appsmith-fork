---
Title: Video
Description: Video widget reference
---

<!--
README

For guidance on how to write documenation, see https://dev.stage.spread.ai/docs/contributor/guide.html. Contact Documentation when this document is ready for review.
-->

This page provides information on using the Video widget, which allows playback of various URLs, including file paths, YouTube, Facebook, Twitch, SoundCloud, Streamable, Vimeo, Wistia, Mixcloud, and DailyMotion.

## Content properties

These properties are customizable options present in the property pane of the widget, allowing users to modify the widget according to their preferences.

### Data

#### URL `string`

Allows you to set the video source to be played, supporting both URL and IPv4-based addresses:

* **IP Based:** `127.0.0.10:8080/path/to/video.mp4`
* **URL Based:** `https://assets.docs.spread.ai/widgets/bird.mp4`

You can display dynamic data by binding the response from a query or a JavaScript function to the **URL** property. For instance, if you have a table with a column containing video URLs, clicking on a specific row plays the corresponding video:

```js
{{ '{{Table1.selectedRow.videoURL}}' }}
```

### General

#### Auto Play `boolean`

Allows you to play the video automatically on page load, without requiring any action from the user. Default value is `false`.

#### Visible `boolean`

Controls the visibility of the widget. If you turn off this property, the widget would not be visible in View Mode. Additionally, you can use JavaScript by clicking on **JS** next to the **Visible** property to conditionally control the widget's visibility. The default value for the property is `true`.

For example, if you want to make the widget visible only when the user selects "Yes" from a Select widget, you can use the following JavaScript expression:

```js
{{ '{{Select1.selectedOptionValue === "Yes"}}' }}
```

#### Animate Loading `boolean`

This property controls whether the widget is displayed with a loading animation. When enabled, the widget shows a skeletal animation during the loading process. Additionally, you can control it through JavaScript by clicking on the **JS** next to the property. The default value for the property is `true`.

### Events

When the event is triggered, these event handlers can execute queries, JavaScript functions, or other [supported actions](/reference/framework/global-functions.md).

#### onPlay

Specifies the action to be executed when the video starts playing.

#### onPause

Specifies the action to be performed when the video is paused.

#### onEnd

Specifies the action to be taken when the video playback is completed.

## Style properties

Style properties allow you to change the look and feel of the widget.

### Color

#### Background Color `string`

Sets the background color of the widget, specified as a [CSS color value](https://developer.mozilla.org/en-US/docs/Web/CSS/color). It can also be manipulated programmatically using the JavaScript functions.

### Border and shadow

#### Border radius `string`

Applies rounded corners to the outer edge of the widget. To control the border radius programmatically, click the **JS** button to enable JavaScript and specify a valid [CSS border-radius](https://developer.mozilla.org/en-US/docs/Web/CSS/border-radius) to adjust the radius of the corners.

#### Box Shadow `string`

This property adds a drop shadow effect to the frame of the widget. To control the Box Shadow programmatically, click the **JS** button to enable JavaScript and specify a valid [CSS box-shadow](https://developer.mozilla.org/en-US/docs/Web/CSS/box-shadow) values to customize the appearance of the shadow.

## Reference properties

Reference properties are properties that are not available in the property pane but can be accessed using the dot operator in other widgets or JavaScript functions. They provide additional information or allow interaction with the widget programmatically. For instance, to get the visibility status, you can use `Video1.isVisible`.

#### autoPlay `boolean`

Indicates the current state of the widget's **Auto Play** setting.

```js
{{ '{{Video1.autoPlay}}' }}
```

#### playState `string`

Indicates the current state of the Video widget's playback. It is represented by a string with values:

* PLAYING: Indicates that the video is currently playing.
* NOT_STARTED: Represents the state when the video has not started playing yet.
* PAUSED: Indicates that the video is paused.
* ENDED: Represents the state when the video playback has ended.

```js
{{ '{{Video1.playState}}' }}
```

#### playing `boolean`

Indicates the current playing state of the widget. When the value is `true`, it means the video is playing.

```js
{{ '{{Video1.playing}}' }}
```

## Methods

Widget property setters enable you to modify the values of widget properties at runtime, eliminating the need to manually update properties in the editor.

These methods are asynchronous and return a [Promise](/writing-code-in-studio/using-js-promises.md). You can use the `.then()` block to ensure execution and sequencing of subsequent lines of code in Studio.

#### setVisibility (param: boolean): Promise

Sets the visibility of the widget.

```js
Video1.setVisibility(true)
```

#### setURL (param: string): Promise

Sets the URL of the video to be displayed in the widget.

```js
Video1.setURL('<https://example.com/video.mp4>')
```

#### setPlaying (param: boolean): Promise

Sets the playing state of the Video widget.

```js
Video1.setPlaying(true)
```
