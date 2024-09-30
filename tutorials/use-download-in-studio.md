---
title: How to use the download function
description: How to use the download function in Studio
---

<!--
README

For guidance on how to write documenation, see https://dev.stage.spread.ai/docs/contributor/guide.html. Contact Documentation when this document is ready for review.
-->

## Synopsis

The [download](../reference/framework/global-functions.md#download) function is a versatile tool within Studio applications that allows users to download data in different formats directly to their local devices. It integrates seamlessly with the `downloadjs` library to facilitate the downloading process, providing flexibility in exporting various data formats, such as text, CSV, JSON, images, and more.

The `download()` function is a powerful and flexible tool that allows users to export and download various types of data. Whether you are exporting JSON data as CSV or downloading images and PDFs, this function provides a seamless method for managing file downloads in Studio applications. With support for multiple formats and customizable file names, it’s an essential function for delivering data to users in a flexible way.

## Prerequisite knowledge

- [x] Basic understanding of how to [build Studio applications](../creating-studio-applications.md).
- [x] Access to a SPREAD Studio environment.
- [x] Data structured in a format that can be downloaded (for example, JSON, text, and so on).

## How the `download()` function works

The structure of the `download()` function is:

```javascript
download(data, fileName, fileType)
```

| Parameter | Description |
| --- | --- |
| **data** | The content to download. This can be a URL, query data, a Blob, or a string. It can also be passed dynamically using mustache binding, such as `{{ '{{UserQuery.data}}' }}`. |
| **fileName** | The name you want to give the downloaded file. You can set this manually or generate it dynamically based on the query or user input (for example, `{{ '{{Table1.selectedRow.id}}' }}`). If no file name is provided, the download will not start.|
| **fileType** | Specifies the [MIME type](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/MIME_types/Common_types) of the file. If not set, the correct file extension should be part of the file name to ensure proper download (for example, `file.csv`). Values can be plain text (TXT), HTML, CSV, JSON, JPEG (and JPG), PNG, SVG, or Excel spreadsheet (XLSX). |

!!! info "Converting file types"

     The `download()` function doesn’t automatically convert data into different formats. For instance, if you want to export a CSV file from JSON, the data must be converted manually using JavaScript before passing it to the `download()` function.

## Instructions

### 1. Download data

You can export query data to a file, such as CSV or TXT file, using the `download()` function. Here’s an example:

   ```javascript
   download(UserData.data, 'UserData.csv', 'text/csv');
   ```

### 2. Downloading data from a URL

To download data from a URL, you can download the file by passing the URL to the function:

   ```javascript
   download(UsersTable.selectedRow.documentUrl, UsersTable.selectedRow.id + '.pdf');
   ```

### 3. Converting data before downloading

If you need to transform your data before exporting, you can use JavaScript to format it accordingly. For example, converting JSON to CSV:

   ```javascript
   const jsonData = userdata.data;
   let csvData = jsonData.map(row => `${row.id},${row.name},${row.email},${row.country}`).join('\n');
   download(csvData, 'users.csv', 'text/csv');
   ```

### 4. Downloading data as a Blob

You can also download binary data using Blobs, for example, to download a PDF:

   ```javascript
   const data = getPdf.data;
   const blob = new Blob([data], {type: 'application/pdf'});
   const url = URL.createObjectURL(blob);
   await download(url, 'sample.pdf', 'application/pdf');
   ```

Ensure the data is served over HTTPS to prevent errors, and make sure the server supports CORS to avoid cross-origin issues.

### 5. Exporting as Excel

The `download()` function also supports exporting data in XLSX format. Here’s how you can export an array of objects or use a pages object structure with specific columns:

```json title="Array of objects"
[
     { "Name": "John", "Age": 30 },
     { "Name": "Jane", "Age": 25 }
]
```

```json title="Pages object with defined column names"
{
     "Sheet1": {
          "columns": [
               { "header": "Name", "key": "name" },
               { "header": "Age", "key": "age" },
               { "header": "City", "key": "city" }
          ],
          "data": [
               { "name": "Alice", "age": 30, "city": "New York" },
               { "name": "Bob", "age": 25, "city": "Los Angeles" }
          ]
          },
          "Sheet2": {
          "columns": [
               { "header": "Product", "key": "product" },
               { "header": "Price", "key": "price" },
               { "header": "Quantity", "key": "quantity" }
          ],
          "data": [
               { "product": "Laptop", "price": 1200, "quantity": 5 },
               { "product": "Phone", "price": 800, "quantity": 10 }
          ]
     }
}
```
