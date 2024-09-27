---
Title: Maps
Description: Maps widget reference
---

<!--
README

For guidance on how to write documenation, see https://dev.stage.spread.ai/docs/contributor/guide.html. Contact Documentation when this document is ready for review.
-->

This page provides information on using the Map widget (powered by [Google Maps API](https://developers.google.com/maps/documentation)) to display location data and enable users to add markers, search, and select locations on the map.

## Content properties

These properties are customizable options present in the property pane of the widget, allowing users to modify the widget according to their preferences.

### Data

#### Initial location	`object`

Sets the default location that the map focuses on when it is displayed for the first time to the user.

If you want to show New York City as the initial location on the Map widget, you can either select it from Google's autocomplete suggestions or define its location using JavaScript:

```js
{
     "lat": 40.7127753,
     "long": -74.0059728,
     "title": "New York, NY, USA"
}
```

#### Default markers `array<object>`

Allows you to display precise locations or display multiple locations at once. To add markers to the Map widget, define an array of markers with latitude, longitude, title and color keys, and set it in the **Default markers** property.

```js
[
     {
          "lat": 25.122, // (1)!
          "long": 50.132, // (2)!
          "title": "Location1", // (3)!
          "color": "green" // (4)!
     }
]
```

1. Latitude of the location.
2. Longitude of the location.
3. Title or name of the location.
4. Color of the marker representing the location.

You can display dynamic data from queries or JavaScript functions by binding the response to the **Default markers** property.

Suppose you want to display multiple markers on a Map using the locations from the users' database:

```js
{{ '{{fetchUserData.data.map(loc  => {
	return {
		lat: parseFloat(loc.latitude),
		long: parseFloat(loc.longitude),
		title: loc.name
	}
})}}' }}
```

This code converts `fetchUserData` into a new array with latitude, longitude, and location name properties.

If you want to display the live location, you can use the **Default Marker** property to set a marker at your current latitude and longitude coordinates. To do this, you can use the following code:

```js
[
     {
          "lat": {{ '{{appsmith.geolocation.currentPosition.coords.latitude || ""}}' }}, 
          "long": {{ '{{appsmith.geolocation.currentPosition.coords.longitude || ""}}' }}
     }
]
```

To fetch the current location, use `appsmith.geolocation.watchPosition()` action triggered by a Button widget's **onClick** event.

### General

#### Zoom Level `number`

Sets the zoom level of the map. Default value is set to `50%`.

#### Visible `boolean`

Controls the visibility of the widget. If you turn off this property, the widget would not be visible in View Mode. Additionally, you can use JavaScript by clicking on **JS** next to the **Visible** property to conditionally control the widget's visibility. Default value is set to `true`.

For example, if you want to make the widget visible only when the user selects "Yes" from a Select widget, you can use the following JavaScript expression:

```js
{{ '{{Select1.selectedOptionValue === "Yes"}}' }}
```

#### Animate Loading `boolean`

This property controls whether the widget is displayed with a loading animation. When enabled, the widget shows a skeletal animation during the loading process. Additionally, you can control it through JavaScript by clicking on the **JS** next to the property. Default value is set to `true`.

#### Enable pick location	`boolean`

Enabling this option allows users to interactively select a location on the map, and the map marker is moved to the user's current location. The `selectedMarker` field is updated with the information of the marker representing the user's current location.

#### Map and Marker Centring `boolean`

When enabled, this setting controls whether the clicked marker is automatically centered on the map.

#### Enable clustering `boolean`

When enabled, groups nearby markers into a single cluster on the map.

#### Enable search location `boolean`

When this property is enabled, a search bar is added to the map, allowing users to easily navigate and search for specific locations. This can be achieved using Google Autocomplete, which suggests potential locations as the user types in the search bar.

To access the searched location, use the ``center`` reference property. This returns the latitude and longitude coordinates of the location. To display the searched location on the map, add the following code to the **Default markers** property:

```js
[
  {{ '{{Map1.center}}' }}
]
```

#### Enable map types `boolean`

When enabled, this property allows users to switch between the default map view and satellite view.

### Create marker

#### Create new marker `boolean`

Allows users to mark locations by adding new markers on the map.

#### onMarkerCreated

This event is available only when the **Create new marker** property is turned on. It specifies the action (Framework functions, queries, or JavaScript functions) to be executed when the user creates a new marker on the map.

### Events

#### onMarkerClick

Sets the action (Framework functions, queries, or JavaScript functions) to be executed when the user clicks a marker on the map.

## Style properties

Style properties allow you to change the look and feel of the widget.

### Border and shadow

#### Border radius `string`

Applies rounded corners to the outer edge of the widget. If JavaScript is enabled, you can specify valid [CSS border-radius](https://developer.mozilla.org/en-US/docs/Web/CSS/border-radius) to adjust the radius of the corners.

#### Box Shadow `string`

This property adds a drop shadow effect to the frame of the widget. If JavaScript is enabled, you can specify valid [CSS box-shadow](https://developer.mozilla.org/en-US/docs/Web/CSS/box-shadow) values to customize the appearance of the shadow.

## Reference properties

Reference properties are properties that are not available in the property pane but can be accessed using the dot operator in other widgets or JavaScript functions. They provide additional information or allow interaction with the widget programmatically. For instance, to get the visibility status, you can use `Map1.isVisible`.

#### isVisible `boolean`

Reflects whether the widget is visible or not.

```js
{{ '{{Map1.isVisible}}' }}
```

#### center `object`

Contains title, latitude, and longitude coordinates of the location.

```js
{{ '{{Map1.center}}' }}
```

#### selectedMarker `object`

Contains the marker object that the user has selected.

```js
{{ '{{Map1.selectedMarker}}' }}
```

#### markers `array<object>`

This contains the list of markers on the map

```js
{{ '{{Map1.markers}}' }} // (1)!
{{ '{{Map1.markers[0].title}}' }} // (2)!
```

1. Access the entire array of markers.
2. Access the title of the first marker in the array.

## Methods

Widget property setters enable you to modify the values of widget properties at runtime, eliminating the need to manually update properties in the editor.

These methods are asynchronous and return a [Promise](/writing-code-in-studio/using-js-promises.md). You can use the `.then()` block to ensure execution and sequencing of subsequent lines of code in Studio.

#### setVisibility (param: boolean): Promise

Sets the visibility of the widget.

```js
MapChart1.setVisibility(true)
```
