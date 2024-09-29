---
title: Set up server-side pagination with a Table
description: Set up server-side pagination with a Table in Studio.
---

<!--
README

For guidance on how to write documenation, see https://dev.stage.spread.ai/docs/contributor/guide.html. Contact Documentation when this document is ready for review.
-->

This page shows you how to set up server-side pagination on a [Table](/reference/widgets/table.md) widget, which allows you to manage and display large datasets within your application. It involves fetching and displaying only a portion of data from the server at a time, which enhances performance.

If you are using the one-click binding feature to connect data, Studio automatically generates server-side pagination queries for you. However, if you prefer to manually configure the server-side setup, you can do so by following the instructions in this guide.

## Prerequisite knowledge

- [x] Basic understanding of how to [build Studio applications](../creating-studio-applications.md).
- [x] Access to a SPREAD Studio environment.
- [x] A Table widget to use in the Studio canvas.

## Instructions

Most databases and APIs support server-side pagination, although the methods of implementation can vary. Studio can handle query responses of up to 5 MB. Server-side pagination can be implemented using:

- **Offset-based pagination:** Offset-based pagination works by using the page number and size to calculate the offset of records to fetch from a database or API.
- **Cursor-based pagination:** Cursor-based pagination is a method that uses unique identifiers (cursors) to navigate and fetch data in large datasets.

### 1. Configure a query

=== Offset-based pagination
    
     Create a query to fetch data from the database or API using `pageSize`, `pageNo`, and `pageOffset` reference properties to implement pagination. For example, for the REST API, the page number can be passed as a query parameter to retrieve the corresponding subset of data, as shown in the URL:

     ```html
     https://mock-api.docs.spread.ai/users?page={{ '{{Table1.pageNo}}' }}
     ```

=== Cursor-based pagination

The cursor serves as a reference point, and you query for a specific number of records that come after or before that cursor. Create a query to fetch data from the database or API using `previousPageVisited` and `nextPageVisited` reference properties to implement pagination. For example, for the REST API, you can make use of the URL's query parameter to retrieve data under specific conditions using `next` and `previous`:

```html
https://api.site.com/users/?pageDirection={{ '{{Table1.nextPageVisited ? "next" : Table1.previousPageVisited? "previous":"default"}}' }} 
```

The `pageDirection` serves as a query parameter within the API.


### 2. Configure the Table widget

Follow these steps to configure the Table widget to display fetched data, and implement server-side pagination:

1. Bind the query data into the [**Table data**](/reference/widgets/table#table-data-arrayobject) property of the Table widget.

```js
{{ '{{fetchData.data}}' }}
```

2. Enable the [**Server-side pagination**](/reference/widgets/table#server-side-pagination-boolean) property in the table.

3. Set the Table widget's [**onPageChange**](/reference/widgets/table#onpagechange) event to run the pagination query. With this setup, users can paginate through data, ensuring an efficient browsing experience.

### 3. Configure total records

To provide the user with information about the number of records in the table, you can configure the [**Total records**](/reference/widgets/table#total-records-number) property to be displayed in the table header.

1. Create a query to fetch the total record count. For example, with PostgreSQL:

```sql
SELECT COUNT(*) from users where name ilike '%{{ '{{Table1.searchText}}' }}%';
```

This SQL query uses the `ilike` condition on the `name` column, pinpointing relevant data rather than performing a blanket count of all records. To display the count, add the following code to the **Total records** property:

```js
{{ '{{fetch_users_count.data[0].count}}' }}
```

2. To display the count, add the following code to the **Total records** property:

```js
{{ '{{fetch_users_count.data[0].count}}' }}
```