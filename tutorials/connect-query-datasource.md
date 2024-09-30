---
title: Connecting a datasource and querying data
description: Learn how to connect a datasource and query data in Studio.
---

<!--
README

For guidance on how to write documenation, see https://dev.stage.spread.ai/docs/contributor/guide.html. Contact Documentation when this document is ready for review.
-->

This tutorial takes you through the process of connecting a datasource and querying data on Studio.

## Prerequisite knowledge

- [x] Basic understanding of how to [build Studio applications](../creating-studio-applications.md).
- [x] Access to a SPREAD Studio environment.

## Instructions

### 1. Connect the datasource

1. In your application, go to the sidebar and click the **Data** button.
2. Select the **+** icon next to **Datasources in your workspace** to add a new datasource.
3. Select **PostgreSQL** under the **Databases** section (or your preferred datasource). This opens the page where you can configure the fields to connect to your PostgreSQL database. 
4. Rename the default database name from **Untitled datasource 1** to `usersTutorialDB`. You may have to click the pencil icon next to the database name if it is not already selected. 
5. Enter the following details in the connection parameter fields:
  * **Host Address**: `mockdb.internal.docs.appsmith.com` 
  * **Port**: `5432`
  * **Database Name**: `users`
  * **Username**: `users`
  * **Password**: `new-users-db-pass`
6. Select the **Test Configuration** button to test the connection and ensure the database is valid.
2. Select **Save** to create and save the database connection. You'll see the `usersTutorialDB` database page.

### 2. Query data

1. In the **Editor pane** click the **New Query/API** button and select the connected datasource. You will see the query editor with a default fetch query to pull ten records from the `usersTutorialDB` database table.
2. Rename the query from **Query1** to `getUsers`. You may have to click the pencil icon if it is not already selected.
3. For this tutorial, modify the query as shown below to fetch the records in the ascending order of the `id` field.

```sql
SELECT * FROM public."users" ORDER BY id LIMIT 10;
```

4. Select the **Run** button on the top right of the screen to execute the query and confirm that it returns data.
5. Select the **Settings** tab. Switch on the **Run query on page load** option.

You've created your first query to fetch the list of records in the database.

### 3. Display data in Table

1. Select the **UI** tab in the **Entity Explorer** to the left of the screen.
2. Select **+ New UI element** and drag a **Table** widget and drop it to the left of the canvas.
3. A property pane appears to the right of the screen, which contains all the properties of the widget. At the top of the property pane, select the default name **Table1** and rename it to `usersTable`.
4. Connect the Table to the query **getUsers** to display the data. Additionally, you can use JavaScript by clicking on **JS** to write bindings for the table data.

You've displayed the results from the **getUsers** query on the Table widget.