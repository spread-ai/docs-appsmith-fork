---
title: Using JSObjects
description: A primer on using and managing JSObjects (or JavasCript Objects)
---

<!--
README

For guidance on how to write documenation, see https://dev.stage.spread.ai/docs/contributor/guide.html. Contact Documentation when this document is ready for review.
-->

JSObjects, or JavaScript Objects, in Studio are powerful tools that enable developers to encapsulate JavaScript code, including functions and variables, to enhance the capability of their applications. They serve the purpose of segregating business logic, performing complex data manipulations, and interacting seamlessly with Studio's widgets and back-end services.

## Defining a JSObject

To define a JSObject in Studio, you need to create a JavaScript module that contains an object that exports specific functions and variables. It's important to note that a JSObject can only export one default object. Here is the general structure of a JSObject:

```javascript
export default {
  // Exported functions and variables go here
};
```

Within this default object, you can define all your reusable code and state that can be accessed throughout the application.

## Functions in JS Objects

JSObjects can contain different types of function definitions.

=== "Arrow syntax"

     ```javascript
     export default {
     calculateArea: (length, width) => length * width,
     };
     ```

=== "Traditional syntax"

     ```javascript
     export default {
     calculateArea: function (length, width) {
     return length * width;
     },
     };
     ```

=== "ES6 function syntax"

     ```javascript
     export default {
     calculateArea(length, width) {
     return length * width;
     },
     };
     ```

## Variables in JS Objects

Variables declared in a JSObject are assigned by value. This means that if you assign a changeable object or a primitive value to a variable within the JSObject, it will not automatically update if the original source changes. To update a variable in the object, you must explicitly re-assign it.

```javascript
export default {
  colorValue: "#4A90E2", // The color value is set when the JSObject is defined
};

// Example of re-assigning the variable
setColorValue: (newColor) => {
  jsObjectName.colorValue = newColor;
};
```

In this example, `colorValue` is initially assigned a hex color code. If later in the application, you want to change this color based on user interaction or some other event, you will have to explicitly call a function like `setColorValue` and pass the new color value as an argument to update `colorValue`.

