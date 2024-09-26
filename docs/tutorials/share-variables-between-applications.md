---
title: Share variables between Studio applications
description: How to share variables between Studio applications.
---

<!--
README

For guidance on how to write documenation, see https://dev.stage.spread.ai/docs/contributor/guide.html. Contact Documentation when this document is ready for review.
-->

## Synopsis

Sometimes you may want to pass a variable from one Studio application to another. For example, you may have a sending application that receives input from a user and sends it to another application, which uses that information for a separate purpose. In this example we will create a simple dialogue between applications using query parameters.

## Prerequisite knowledge

- [x] An understanding of how to [create Studio applications](../creating-studio-applications.md).
- [x] Access to a SPREAD Studio environment.
- [x] A basic understanding of how to [use JavaScript to get input field values](https://simpledev.io/lesson/get-input-value-js/).
- [x] A basic understanding of what [query parameters](https://en.wikipedia.org/wiki/Query_string) are.

## Instructions

### 1. Create a simple sending application

Start by creating a simple Studio application with an input field and button.

<figure markdown="span">
	![A simple application with just an input field and a submit button](../src/sending-application-sharing-variables.png)
	<figcaption>A simple application with just an input field and a submit button</figcaption>
</figure>

<div class="annotate" markdown>Set the name of the input field to `valueToShare`. (1)</div>

1. You can set the name at the top of the property window of the input box, next to the Copy and Trash icons.

### 2. Create a receiving application

Create a receiving application with just an input field and publish it. Got to the launcher page and run the receiving application. Get the URL of the application and save it for the next step. The URL should look something like this:

`https://studio.stage.stage.spread.ai/app/receiving-application/page1-65fa6160dc4fa21cdb10c113`

!!! info "Remove any query parameters in the URL"

    You may have `...?embed=true` at the end of the copied URL. Anything after the `?` is a query parameter and should be removed from the saved URL. We will add query parameters in the next step.

### 3. Set the query parameter in the sending application

Go back to the sending application and inside the widget properties for the submit button add an **onClick** action and select **Navigate to** > **URL**.

<figure markdown="span">
	![Adding an onClick action to navigate to the receiving application](../src/navigate-to-onclick-action.png)
	<figcaption>Adding an onClick action to navigate to the receiving application</figcaption>
</figure>

In the **Enter URL** field enter the URL from [Step 2](#2-create-a-receiving-application). In the **Query params** field enter the following:

``` json title='Query parameters for the sending application' hl_lines='3'
{{ '{{ "embed": true, "sharedVariable": valueToShare.text }}' }}
```

In the highlighted line, the text of the input field is fetched using JavaScriot and used as the value to the `sharedVariable` key.

### 4. Set the input field to the query parameter

Go to the receiving application. In the property window of the input field, set the **Default Value** to:

``` json title='Query parameters for the sending application' hl_lines='3'
{{ '{{appsmith.URL.queryParams.sharedVariable}}' }}
```

This gets the current URL in the receiving application and filters for the query parameter with the `sharedVariable` key.

!!! info "More about the `appsmith` global object"

    The appsmith global object contains information about the application, including the current URL. For more about the information you can get from the object, see [appsmith global object](https://docs.appsmith.com/reference/appsmith-framework/context-object).

Now you can run the sending application, enter a value, submit, and see it reflected in the receiving application.

<br>

[Download the sending application (3kb) :material-download:](../src/sending-app.json.zip){ .md-button .md-button--primary }

<figcaption style='text-align: left; max-width: none'>Unzip the file, and import the JSON inside the Studio application: <b>Create New</b> > <b>Import</b> from the Studio landing page. Change the URL of the receiving application.</figcaption>

<br>

[Download the receiving application (2kb) :material-download:](../src/receiving-app.json.zip){ .md-button .md-button--primary }

<figcaption style='text-align: left; max-width: none'>Unzip the file, and import the JSON inside the Studio application: <b>Create New</b> > <b>Import</b> from the Studio landing page.</figcaption>
