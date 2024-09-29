---
title: Set up server-side pagination with a List
description: Set up server-side pagination with a List in Studio.
---

<!--
README

For guidance on how to write documenation, see https://dev.stage.spread.ai/docs/contributor/guide.html. Contact Documentation when this document is ready for review.
-->

This page shows you how to set up server-side pagination on the List widget, which allows you to manage and display large datasets within your application. It involves fetching and displaying only a portion of data from the server at a time, which enhances performance.

## Prerequisite knowledge

- [x] Basic understanding of how to [build Studio applications](../creating-studio-applications.md).
- [x] Access to a SPREAD Studio environment.
- [x] A [List](/reference/widgets/list.md) widget to use in the Studio canvas.

## Instructions


### 1. Configure a query

Most databases and APIs support server-side pagination, although the methods of implementation can vary. Create a query to fetch data from the database or API using [pageSize](/reference/widgets/list.md#pagesize-number), and [pageNo](/reference/widgets/list.md#pageno-number) reference properties to implement pagination.

For example, for a REST API, the page number can be passed as a query parameter to retrieve the corresponding subset of data, like:

```api
https://mock-api.docs.spread.ai/users?page={{ '{{List1.pageNo}}' }}
```

### 2. Configure the List widget

Follow these steps to configure the List widget to display fetched data, and implement server-side pagination:

1. Connect the query data to the [**Items**](/reference/widgets/list.md#items-string) property of the List widget.

For example:

```js
{{ '{{fetchData.data}}' }}
```

2. Enable the [**Server-side pagination**](/reference/widgets/list.md#server-side-pagination) property.
3. Set the List widget's [**onPageChange**](/reference/widgets/list.md#onpagechange) event to run the pagination query.


### 3. Configure total records

To provide the user with information about the number of records in the List, you can configure the [**Total records**](/reference/widgets/list.md#total-records-number) property. The record count is displayed as part of the page number at the bottom of the list.

1. Create a query to fetch the total record count.

For example, with PostgreSQL:

```sql
SELECT COUNT(*) FROM users;
```

This SQL query counts and returns the total number of records (rows) in the `users` table.

2. To display the count, add the following code to the **Total records** property:

```js
{{ '{{fetch_users_count.data[0].count}}' }}
```
