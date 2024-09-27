---
Title: Audio
Description: Audio widget reference
---

<!--
README

For guidance on how to write documenation, see https://dev.stage.spread.ai/docs/contributor/guide.html. Contact Documentation when this document is ready for review.
-->

This page provides information on using the Audio widget to play MP3, WAV, OGG audio files. It also supports URLs from YouTube, Facebook, Twitch, SoundCloud, Streamable, Vimeo, Wistia, Mixcloud, and DailyMotion.

## Content properties

These properties are customizable options present in the property pane of the widget, allowing users to modify the widget according to their preferences.

### Data

#### URL `string`

Allows you to set the audio source to be played. It supports various formats such as MP3, WAV, and OGG.

```js
https://assets.spread.ai/widgets/birds_chirping.mp3
```

You can display dynamic data by binding the response from a query or a JavaScript function to the **URL** property. For instance, if you have a table with a column containing audio URLs, clicking on a specific row plays the corresponding audio:

```js
{{ '{{Table1.selectedRow.audioURL}}' }}
```

### General

#### Auto Play `boolean`

Enables the audio to play automatically on page load, without requiring any action from the user. Default value is `false`.

#### Visible `boolean`

Controls the visibility of the widget. If you turn off this property, the widget would not be visible in View Mode. Additionally, you can use JavaScript by clicking on **JS** next to the **Visible** property to conditionally control the widget's visibility. The default value for the property is `true`.

For example, if you want to make the widget visible only when the user selects "Yes" from a Select widget, you can use the following JavaScript expression:

```js
{{ '{{Select1.selectedOptionValue === "Yes"}}' }}
```

#### Animate Loading `boolean`

This property controls whether the widget is displayed with a loading animation. When enabled, the widget shows a skeletal animation during the loading process. Additionally, you can control it through JavaScript by clicking on the **JS** next to the property. The default value for the property is `true`.

### Events

When the event is triggered, these event handlers can execute queries, JS functions, or other [supported actions](/reference/framework/global-functions.md).

#### onPlay

Specifies the action to be executed when the audio starts playing.

#### onPause

Specifies the action to be performed when the audio is paused.

#### onEnd

Specifies the action to be taken when the audio playback is completed.

## Reference properties

Reference properties are properties that are not available in the property pane but can be accessed using the dot operator in other widgets or JavaScript functions. They provide additional information or allow interaction with the widget programmatically. For instance, to get the visibility status, you can use `Audio1.isVisible`.

#### autoPlay `boolean`

Indicates the current state of the widget's **Auto Play** setting.

```js
{{ '{{Audio1.autoPlay}}' }}
```

#### playState `string`

Indicates the current state of the Audio widget's sound playback. It is represented by a string with values:

* PLAYING: Indicates that the audio is currently playing.
* NOT_STARTED: Represents the state when the audio has not started playing yet.
* PAUSED: Indicates that the audio is paused.
* ENDED: Represents the state when the audio playback has ended.

```js
{{ '{{Audio1.playState}}' }}
```

#### playing `boolean`

Indicates the current playing state of the widget. When the value is `true`, it means the audio is playing.

```js
{{ '{{Audio1.playing}}' }}
```

## Methods

Widget property setters enable you to modify the values of widget properties at runtime, eliminating the need to manually update properties in the editor.

These methods are asynchronous and return a [Promise](/writing-code-in-studio/using-js-promises.md). You can use the `.then()` block to ensure execution and sequencing of subsequent lines of code in Studio.

#### setPlaying (param: boolean): Promise

Updates the playing state of the Audio widget. When the `setPlaying` method is called with `true`, the audio starts playing, and when called with `false`, the audio stops playing.

```js
Audio1.setPlaying(true)
```

#### setURL (param: string): Promise

Updates the URL of the audio to be played in the audio widget. Provide the desired URL as a string parameter to the `setURL` method.

```js
Audio1.setURL('<https://example.com/audio.mp3>')
```

#### setVisibility (param: boolean): Promise

Updates the visibility of the Audio widget.

```js
Audio1.setVisibility(true)
```
