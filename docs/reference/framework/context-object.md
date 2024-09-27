---
title: Context object
description: The Context object provides information about the current state of the application.
---

<!--
README

For guidance on how to write documenation, see https://dev.stage.spread.ai/docs/contributor/guide.html. Contact Documentation when this document is ready for review.
-->

The `appsmith` object is a global object that provides access to information and functionalities within an application through objects and utility functions.

## Properties

The `appsmith` object has the following properties.

### Store `object`

This object lets you access any app-level data or temporary state that is stored on the user's browser. You can add or update data using the [storeValue()](/reference/framework/global-functions.md/store-value) method. You can access saved data by referencing their keys:

```javascript
{{ '{{ appsmith.store.KEY_NAME }}' }}
```

### URL

This object has all the attributes of the current URL that the user is on. To access these values from the URL, you can use the following code snippet:

```javascript
{{ '{{ appsmith.URL }}' }}
```

The URL object has the following attributes:

#### host `string`

The host property of the URL is a string that consists of the hostname and the URL's port (if available). To access the host value, you can use the following code snippet:

```js
{{ '{{appsmith.URL.host}}' }}
```
  
#### hostname `string`

The hostname property of the URL is a string that represents the URL's domain. In simpler terms, hostname is the [host](/reference/appsmith-framework/context-object#host) name (without the port number). To access the hostname, you can use the following code snippet:

```js
{{ '{{appsmith.URL.host}}' }}
```

#### fullPath `string`

A full-path URL specifies the exact location of a resource, such as a page, app, file, or any other specific entity. A full-path URL includes the following components:

* Protocol
* Subdomain
* Domain Name
* Top-Level Domain (TLD)
* Path
* Parameters

You can access the `fullPath` using the following snippet:

```js
{{ '{{appsmith.URL.fullPath}}' }}
```

#### pathname `string`

The pathname is a string that represents the path component of the URL. It consists of a collection of path segments, with each segment prefixed by the `/` character. If the URL does not have any path segments, the value of the pathname property is an empty string. You can access the pathname using the following snippet:

```js
{{ '{{appsmith.URL.pathname}}' }}
```

#### port `string`

The URL's port property is a string containing the URL's port number. You can access the port using the following snippet:

```js
{{ '{{appsmith.URL.port}}' }}
```

#### protocol `string`

The protocol property of the URL is a string that represents the protocol scheme of the URL, including the `:`. The protocol identification and the resource name are separated by a colon and two forward slashes (`://`). To access the protocol value, use the following snippet:

```js
{{ '{{appsmith.URL.protocol}}' }}
```

#### hash `string`

The value of the `appsmith.URL.hash` property is a string that represents the fragment identifier of the URL, including the `#` character. The fragment identifier is the portion of the URL that appears after the hashtag symbol (#), which is the hash property of the URL interface.

```js
{{ '{{appsmith.URL.hash}}' }}
```

#### queryParams `object`

The query parameters are a component of a URL that allows for passing data to a web server or application. In a URL, query parameters are appended at the end of the URL with a `?` as a separator. You can access the value of `queryParams` using the following snippet:

```js
{{ '{{appsmith.URL.queryParams}}' }}
```

The `queryParams` object can be used to [share data across pages](/advanced-concepts/sharing-data-across-pages#sharing-data-via-query-params).

### user `object`

This object has the data of the currently authenticated user.

```javascript
{
     "email": string,
     "username": string,
     "name": string,
     "useCase": string,
     "enableTelemetry": boolean,
     "roles": object,
     "groups": object,
     "accountNonExpired": boolean,
     "accountNonLocked": boolean,
     "credentialsNonExpired": boolean,
     "emptyInstance": boolean,
     "isAnonymous": boolean,
     "isEnabled": boolean,
     "isSuperUser": boolean,
     "isConfigurable": boolean,
     "adminSettingsVisible": boolean,
     "isIntercomConsentGiven": boolean
}
```

#### email `string`

The `email` property of user has the email address of the user.
To access the email, use the following code:

```javascript
{{ '{{appsmith.user.email}}' }}
```

#### username `string`

The `username` attribute represents the unique username associated with the user's account.
To access the username, use the following code:

```javascript
{{ '{{appsmith.user.username}}' }}
```

#### name `string`

The `name` attribute holds the full name of the user. To access the name, use the following code:

```javascript
{{ '{{appsmith.user.name}}' }}
```

#### useCase `string`

This attribute describes the use case that the user has specified, giving insight into what they intend to achieve with Studio. To access the `useCase`, use the following code:

```javascript
{{ '{{appsmith.user.useCase}}' }}
```

#### enableTelemetry `boolean`

This boolean flag indicates if the user has consented to send telemetry data to Studio. Telemetry data typically includes usage statistics and error reports that help improve the platform. To access the `enableTelemetry`, use the following code:

```javascript
{{ '{{appsmith.user.enableTelemetry}}' }}
```

#### roles `object`

This object has an array of strings of the roles assigned to the currently authenticated user. You can access the value of roles using the snippet given below:

```js
appsmith.user.roles
```

It returns an array of all the roles in your instance. For example:

```javascript
[
     "Instance Administrator Role",
     "Default Role For All Users",
     "Administrator",
     "Custom Role-1",
     "Custom Role-2"
]
```

You can use `appsmith.user.roles` object to programmatically control the access to your application entities.

For example, consider a scenario where you are hiding a **Button** widget by adding the following code to the **Visible** property of the button:

```javascript
{{ '{{appsmith.user.roles.includes("back-end engineers")}}' }}
```

In the above example, the visibility of the button is determined by a role. Only users who have been assigned the "back-end engineer" role can see this button.

#### groups `object`

This object has an array of strings of the groups assigned to the currently authenticated user. You can access the value of groups using the snippet given below:

```js
appsmith.user.groups
```

It returns an array of all the groups in your instance. For example:

```javascript
[
     "Administrators",
     "Managers",
     "End Users" 
]

```

You can use `appsmith.user.groups` object to programmatically control the access to your application entities.

For example, consider a scenario where you are hiding a Button widget by adding the following code to the **Visible** property of the button -

```javascript
{{ '{{appsmith.user.groups.includes("managers")}}' }}
```

In the above example, the visibility of the button is determined by a group. Only users who have been added to the "managers" group can see this button.

#### accountNonExpired `boolean`

This attribute indicates whether the user's account is still active and has not expired. An expired account may be reactivated or may need subscription renewal. To access the `accountNonExpired`, use the following code:

```javascript
{{ '{{appsmith.user.accountNonExpired}}' }}
```

#### accountNonLocked `boolean`

The `accountNonLocked` attribute signifies whether the user's account is locked or unlocked. A locked account cannot be accessed until an administrator unlocks it. To access the `accountNonLocked`, use the following code:

```javascript
{{ '{{appsmith.user.accountNonLocked}}' }}s
```

#### credentialsNonExpired `boolean`

This boolean attribute states if the user's credentials (such as their password) are still valid or if they need to be updated. Expired credentials typically require the user to reset their password. To access the `credentialsNonExpired`, use the following code:

```javascript
{{ '{{appsmith.user.credentialsNonExpired}}' }}
```

#### emptyInstance `boolean`

The `emptyInstance` attribute indicates whether this user object is an empty instance, lacking in actual data. This might occur when no user is logged in or in case of a system-level operation. To access the `emptyInstance`, use the following code:

```javascript
{{ '{{appsmith.user.emptyInstance}}' }}
```

#### isAnonymous `boolean`

The `isAnonymous` attribute reflects whether the current user is anonymous (not logged in) or identified (logged in). This can affect the presentation and permissions of the user interface. To access the `isAnonymous`, use the following code:

```javascript
{{ '{{appsmith.user.isAnonymous}}' }}
```

#### isEnabled `boolean`

This attribute indicates if the user's account is currently enabled. An enabled account can log in and interact with Studio applications, while disabled ones cannot. To access the `isEnabled`, use the following code:

```javascript
{{ '{{appsmith.user.isEnabled}}' }}
```

#### isSuperUser `boolean`

The `isSuperUser` flag shows whether the user has superuser status. Superusers typically have elevated privileges and access to all parts of the Studio application. To access the `isSuperUser`, use the following code:

```javascript
{{ '{{appsmith.user.isSuperUser}}' }}
```

#### isConfigurable `boolean`

This attribute denotes whether the user has the ability to configure or alter settings within the Studio platform. To access the `isConfigurable`, use the following code:

```javascript
{{ '{{appsmith.user.isConfigurable}}' }}
```

#### adminSettingsVisible `boolean`

The `adminSettingsVisible` attribute states if the user is able to see and possibly modify the admin settings area. To access the `adminSettingsVisible`, use the following code:

```javascript
{{ '{{appsmith.user.adminSettingsVisible}}' }}
```

#### isIntercomConsentGiven `boolean`

This boolean indicates whether the user has given consent to use Intercom, a messaging tool that might be used in Studio for support and communication purposes. To access the `isIntercomConsentGiven`, use the following code:

```javascript
{{ '{{appsmith.user.isIntercomConsentGiven}}' }}
```

#### idToken `object`

An ID token serves as a verified confirmation of a user's identity and includes essential information such as their name, picture, email address and so on According to the OpenID Connect (OIDC) specifications, when a user successfully logs in, Studio receives an ID token.

Studio provides the `idToken` parameter on the client side, allowing you to incorporate it into various operations like JavaScript functions, APIs, or queries as needed. You can read the value of an ID token in your APIs/Queries by using the mustache syntax `{{ '{{}}' }}` as shown below:

```js
{{ '{{appsmith.user.idToken}}' }}
```

If you have defined custom scopes in your identity provider, the information associated with those scopes can be accessed within the Identity token.

### theme `object`

This object has the details of the theme properties applied to the application. You can use this object to set certain properties in widgets to be aligned with the app theme or to write custom logic.

```js
{{ '{{appsmith.theme}}' }}
```

The theme object has the following attributes:

#### colors `object`

This object has the color properties of the application. It has the following properties:

#### primaryColor `string`

It refers to the app's primary color set in the theme section of the app settings. To access this value, you can use the following code snippet:

```js
{{ '{{appsmith.theme.colors.primaryColor}}' }}
```

#### backgroundColor `string`

The `backgroundColor` property refers to the background color set in the theme section of the app settings. To access the value of the background color, you can use the following code snippet:

```js
{{ '{{appsmith.theme.colors.backgroundColor}}' }}
```

#### borderRadius `object`

This object has the border properties that enable you to control the curvature or roundness of the corners of the widgets in the application.

#### appBorderRadius `string`

It refers to the border radius set in the theme section of the app settings. To access its value, you can use the following code snippet:

```js
{{ '{{appsmith.theme.borderRadius.appBorderRadius}}' }}
```

#### boxShadow `object`

This object allows you to add a shadow effect to the widgets in your application.

#### appBoxShadow `string`

It refers to the box shadow set in the theme section of the app settings. You can access the value of `appBoxShadow` using the following snippet:

```js
{{ '{{appsmith.theme.boxShadow.appBoxShadow}}' }}
```

#### fontFamily `object`

This object has the font properties of your application.

#### appFont `string`

It refers to the font family set for the app in the theme section for app settings. You can access the value of `appFont` using the following snippet:

```js
{{ '{{appsmith.theme.fontFamily.appFont}}' }}
```

### geolocation `object`

This object has functions that allow you to retrieve the current user's location and the coordinates received from the user's device using the [Geolocation API](https://developer.mozilla.org/en-US/docs/Web/API/Geolocation_API).

```javascript
{
     canBeRequested: boolean,
     getCurrentPosition: Function,
     watchPosition: Function,
     clearWatch: Function,
     currentPosition: {
     coords: {
          accuracy: number,
          altitude: number | null,
          altitudeAccuracy: number | null,
          heading: number | null,
          latitude: number,
          longitude: number,
          speed: number | mull,
     },
     timestamp: number,
     }
}
```

#### geolocation.getCurrentPosition()

Signature:

```javascript
(
     onSuccessCallback?,
     onErrorCallback?,
     options?: { maximumAge?: number, timeout?: number, enableHighAccuracy?: boolean } 
) -> void
```

Similar to the original browser API, the `getCurrentPosition` function retrieves the current user's location. However, unlike the original browser API, you don't need to pass a success callback function. On success, the location information is automatically stored at `appsmith.geolocation.currentPosition.coords`. If you provide an `onSuccessCallback` function, it is called with the received location information as a parameter.

#### geolocation.watchPosition()

Signature:

```javascript
(
     onSuccessCallback?,
     onErrorCallback?,
     options?: { maximumAge?: number, timeout?: number, enableHighAccuracy?: boolean } 
) -> void
```

Similar to the original browser API, the `getCurrentPosition` retrieves periodic updates about the current geographic location of the device, with the difference being that you don't need to pass a success callback explicitly. On success, the location is automatically stored at `appsmith.geolocation.currentPosition.coords` and `appsmith.geolocation.currentPosition.timestamp` is also updated to indicate the time of the last position update. If you provide callbacks, they are automatically executed when the location has changed. Unlike the browser API, no `watchId` is returned, as the platform only allows for a single `watchPosition` at a time.

#### geolocation.clearWatch()

Signature: `() -> Promise`

It is similar to the original browser API, with the difference being that you don't have to explicitly pass the `watchId`. Instead, if a watch is currently active, you must clear it before starting a new one.

### mode `enum`

This field is an enum that signals whether the app runs in view or edit mode. It takes the values `VIEW` or `EDIT`.
