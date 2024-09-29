---
title: Download table data
description: Learn how to download table data in Studio.
---

<!--
README

For guidance on how to write documenation, see https://dev.stage.spread.ai/docs/contributor/guide.html. Contact Documentation when this document is ready for review.
-->

This page shows how to download the entire Table or query data in manageable chunks to prevent performance issues on your application.

## Prerequisite knowledge

- [x] Basic understanding of how to [build Studio applications](../creating-studio-applications.md).
- [x] Access to a SPREAD Studio environment.
- [x] Basic knowledge of JavaScript.

## Instructions

### Download data as chunks

1. Create a new query to fetch paginated data. For example, using an API, create back-end code in your API to handle dynamic `limits` and `offsets`:

```js title="Back-end code to fetch data with limit and offset"
const fetchData = async (limit = 50, offset = 0) => {
     const response = await fetch(`/api/endpoint?limit=${limit}&offset=${offset}`);
     const data = await response.json();
     return data;
};
```

2. In Studio, configure the API query to fetch data using `limit` and `offset` parameters:

```js
GET https://mock-api.docs.spread.ai/users?limit={{ '{{this.params.limit}}' }}&offset={{ '{{this.params.offset}}' }}
```

3. Create a new [JSObject](../writing-code-in-studio/using-jsobjects.md) and add a function to fetch the data in chunks to handle large datasets efficiently. For example:

* Create a function that retrieves user data in batches of 100 rows from a database, continuously appending each batch to a `usersData` array until the entire dataset is retrieved.
* Use the [download()](/reference/framework/global-functions.md#download) function to download the data to your local machine.
* Upon successfully fetching and downloading all data, it resets the `usersData` array to clear the data.

```js
export default {
    usersData: [],

    // M
    resetData() { // (1)!
        this.usersData = [];
    },

    async fetchAndDownloadUsers() { // (2)!
        const chunkSize = 100; // (3)!
        let offset = 0; // (4)!

        try {
            while (true) {
                const result = await getUsers.run({ limit: chunkSize, offset });

                if (result && result.length > 0) { // (5)!
                    this.usersData = [...this.usersData, ...result];
                    offset += chunkSize; // (6)!
                
                } else {
                    break; // (7)!
                }
            }

            download(this.usersData, 'userdata', 'text/csv'); // (8)!
            console.log('Data downloaded:', this.usersData);

        } catch (error) {
            console.error('An error occurred:', error);
        } finally {
            this.resetData(); // (9)!
            console.log('Data has been reset:', this.usersData);
    }}' }}
}
```

1. Method to reset variables.
2. Method to fetch and download user data in chunks.
3. Number of rows per chunk.
4. Offset for pagination.
5. Check if the query returned any data.
6. Append the fetched data to `usersData`.
7. No more data available, exit the loop.
8. Download or process the data.
9. Clear the data and reset variables.

The code may vary based on your datasource, so update the query and parameters accordingly to fit your specific data structure and requirements. Execute the defined JS function either directly from the JS editor or by triggering the function through widget events.

## Download data as file

To directly download a file from the datasource instead of fetching data in chunks, follow these steps:

1. Create a back-end API that uses built-in functions provided by your datasource to convert data into a file format. Ensure that the output is either the file content or a URL that provides access to the file.

For example, [MySQL](https://dev.mysql.com/doc/mysql-shell/8.0/en/mysql-shell-utilities-table-export.html), [PostgreSQL](https://www.postgresql.org/docs/current/sql-copy.html), [GraphQL](https://docs.celigo.com/hc/en-us/articles/6223964431003-Export-data-from-GraphQL#Configure_Export), and [AWS DynamoDB](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/S3DataExport_Requesting.html#S3DataExport_Requesting_SDK) offer functionalities to export data directly to files.

2. In Studio, create a new query to connect with the back-end API and access the file. For example:

```js
http://api.example.com/export-data-to-file
```

3. Create a new [JSObject](../writing-code-in-studio/using-jsobjects.md) and add a function to fetch and download the file. For example, If the API provides a file URL, you can download the data by using the following code:

```js
const fileUrl = userAPI.data.fileUrl; // (1)!

// (2)!
const response = await fetch(fileUrl);
const data = await response.blob();
const fileName = 'data.csv';
const fileType = 'text/csv';

// (3)!
await download(data, fileName, fileType);
```

1. Assuming userAPI.data contains the file URL.
2. Fetch the file content.
3. Trigger the download.

The code fetches the file content from this URL, and then triggers `download()` function to download the file.
