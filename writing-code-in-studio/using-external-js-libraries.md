---
title: Using external JavaScript libraries
description: A guide on how to import and use external JavaScript libraries.
---

<!--
README

For guidance on how to write documenation, see https://dev.stage.spread.ai/docs/contributor/guide.html. Contact Documentation when this document is ready for review.
-->

You can install custom libraries to help you build complex applications and business logic. Custom JavaScript libraries enable complex use cases like PDF generation, CSV Parsing, and authentication.

You can find a distribution of the library in either [ECMAScript Modules](https://tc39.es/ecma262/#sec-modules) (ESM) or [Universal Module Definition](https://github.com/umdjs/umd) (UMD) format on a popular CDN service, such as [jsDelivr](https://www.jsdelivr.com/) or [UNPKG](https://unpkg.com/). For more information on library compatibility, see the [Library Compatibility](#library-compatibility) section.

## Built-in JavaScript libraries

Studio provides the following built-in JavaScript libraries that can be utilized in your applications.

### Lodash

 
Lodash provides functions for common programming tasks such as formatting data, iterating over collections, and manipulating arrays and objects.

```
{{ '{{ _.sortBy(fetchUsers.data, ["age"]) }}' }}
```
For more information, see [Lodash](https://lodash.com/docs/4.17.15)

#### Moment

Simplifies working with dates and times in JavaScript by providing functions for parsing, validating, manipulating, and displaying dates and times.

`moment(datePicker1.selectedDate.format('DD MMM'))`

For more information, see [Moment](https://momentjs.com/docs/)

### Forge

Forge can be used to work with cryptographic algorithms and protocols in JavaScript.

```javascript
export default {
  hash() {
    var md = forge.md.sha256.create();
    md.update("The quick brown fox jumps over the lazy dog");
    return md.digest().toHex();
  },
};
```

For more information, see [Forge](https://github.com/digitalbazaar/forge)

## External JS Libraries

You can also [follow this guide](/core-concepts/writing-code/ext-libraries) to install external JavaScript libraries that are not loaded by default into your application.


## Install an external library

Studio provides a set of recommended libraries. To install a recommended library, click the **+** icon next to the library in the library explorer and click the **Install** icon next to it.

Follow these steps if you want to install a specific library that you found online:

<figure markdown="span">
     ![Install external JavaScript libraries](src/appsmith-install-external-libraries.png)
     <figcaption>Install external JavaScript libraries</figcaption>
</figure>

1. Copy the URL to its index file. For example: `https://cdn.jsdelivr.net/npm/exceljs@4.3.0/dist/exceljs.min.js`
2. Go to your Studio app, and click the **library icon** above the **App settings** in the bottom-left corner.
3. Click the **+** icon next to **Installed libraries**.
4. On the **Add JS libraries** pop over, paste the URL into the **Library URL** field. For example, you want to install excelJS library. Paste the URL: `https://cdn.jsdelivr.net/npm/exceljs@4.3.0/dist/exceljs.min.js`
5. Click the **Install** button to install the library. You will see the **ExcelJS** library available under installed Libraries.
6. The installed library can be accessed as an object in your JavaScript code in Studio. If you want to access `excelJS` library in your JS object in a function, you can do that as follows:

      ```javascript
      const workbook = new ExcelJS.Workbook();
      ```

Use the `workbook` variable to perform operations provided by the library on it.

## Library compatibility

Studio supports libraries written in either the [ECMAScript Modules](https://tc39.es/ecma262/#sec-modules) (ESM) or [Universal Module Definition](https://github.com/umdjs/umd) (UMD) pattern. ESM is the standard format for packaging JavaScript code for reuse. ES Modules use import and export statements for defining modules.

For libraries not available in ESM format, look for an index file under the `root`, `/umd`, or `/browser` folders with a `.min.js` extension. You may use [browserify](https://browserify.org/) to generate a UMD build and host it on a CDN of your choice.

## Unsupported libraries

Libraries that fall under the below categories do not meet compatibility requirements and are not supported by Appsmith:

* Manipulate the Document Object Model (DOM).
* Rely on [XMLHttpRequest](https://en.wikipedia.org/wiki/XMLHttpRequest).
* Invoke or require access to some browser methods such as: `setInterval`, `clearInterval`, `localStorage`, `setImmediate`, or `navigator`.
* Are distributed in unsupported build formats, such as plain `.js` files. For example,  `https://cdn.jsdelivr.net/npm/uuid@9.0.0/dist/index.js`.
* Do not point to an index file. Such as: `https://www.jsdelivr.com/package/npm/datejs`.
