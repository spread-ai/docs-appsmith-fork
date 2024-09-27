---
title: Troubleshooting Studio
description: An overview of how to fix and debug Studio applications.
---

<!--
README

For guidance on how to write documenation, see https://dev.stage.spread.ai/docs/contributor/guide.html. Contact Documentation when this document is ready for review.
-->

Understanding how to effectively troubleshoot errors in Studio can save you time and help maintain a smooth development process. Studio errors fall into the following categories. For more on each type, select the relevant section:

* [Datasource errors](#datasource-errors)
* [Query errors](#query-errors)
* [Widget errors](#widget-errors)
* [JavaScript errors](#javascript-errors)
* [Access errors](#access-control-errors)
* [Git errors](#git-errors)

## Access control errors

Access control errors happen when a user cannot access a Studio application or a developer cannot edit an application. This page shows how to troubleshoot some of the most common access control errors you might encounter. Resolving some of these error may require super administrator access.

### Common access control errors

#### 404 - page not found

> The **404 - Page Not Found** error occurs when you do not have access to the requested page. In this case, access to the Home page is not provided, resulting in the error.

<div class='grid' markdown>

!!! failure "Error"

	A **404 - Page Not Found** error page.

!!! success "Solution"

     Verify if the custom role access is provided by checking the groups and role mapping or user and role assignment. If not, add users to groups that have access or assign roles to the appropriate users.

	Contact your instance administrator and request access to application, and maybe the Studio environment. For more information, see [User Management](/platform/user-management/user-management-and-permissions).

</div>

#### Make application public toggle is not available

> The **Make Application Public** toggle is controlled by the **Make Public** permission. If you do not have this permission, the toggle is disabled.

<div class='grid' markdown>

!!! failure "Error"

	The **Make Application Public** toggle in the invite users modal is disabled, preventing you from making an application public.

!!! success "Solution"

     You must contact your instance administrator and request that they provide you with the appropriate access. Alternatively, reach out to users who have the necessary permissions to make an application public.

</div>

## Datasource errors

Studio provides the ability to connect to a variety of data sources, including both databases and APIs. However, when setting up a new datasource or modifying an existing one, you may encounter connectivity errors. This guide aims to help you troubleshoot and resolve common datasource connectivity errors.

### Testing the data source

1. Navigate to your Studio application's datasource page.
2. Find the datasource in question and click on the **Test** button.
3. If the **Test Configuration** option indicates failure, proceed to troubleshoot the datasource connectivity.

### Troubleshooting datasource connectivity

* Ensure that your datasource URL, authentication credentials, and other settings are correctly configured.

* Verify that any IP whitelisting or firewall rules allow traffic from Studio's servers.
* Review any error messages returned by the Test Configuration for clues to the problem.

### Common datasource errors

#### SSL connection error

> This error message indicates that the database server that you are trying to connect to does not support SSL.

<div class='grid' markdown>

!!! failure "Error"

     ```html
	<Message messageContainerClassName="error" 
     messageContent="dev.miku.r2dbc.mysql.client.MySqlConnectionClosedException: Connection unexpectedly closed. Error was received while reading the incoming data. The connection will be closed."/>
     ```

!!! success "Solution"

     This error can be resolved by editing the SSL field in the datasource and setting it to `Disabled`.

</div>

#### Error connecting to local database or API

> If you are trying to connect to a local database from Studio and see an error message. When running Studio inside a Docker container, it may have its own network namespace and won't be able to access services running on the host machine using the `localhost` or `127.0.0.1` addresses. This is because these addresses points to the container's local network, which is different from that of the host machine.

<div class='grid' markdown>

!!! failure "Error"

     ```html
	<Message messageContainerClassName="error" 
     messageContent="Connection refused. Server logs - 'io.netty.channel.AbstractChannel$AnnotatedConnectException: finishConnect(..) failed: Connection refused: /172.17.0.1:3306'"/>
     <Message messageContainerClassName="error" 
     messageContent="dev.miku.r2dbc.mysql.client.MySqlConnectionClosedException: Connection unexpectedly closed. Error was received while reading the incoming data. The connection will be closed."/>
     ```

!!! success "Solution"

     Use the hostname `host.docker.internal` on Windows and macOS hosts, and `172.17.0.1` on Linux hosts, to access services running on the host machine from within the container.

</div>

#### Secret key required error

>When the data source returns an error about the secret key. This message indicates that `Send Studio signature header` field has been marked as `Yes` but the `Session Details Signature Key` field is left empty

<div class='grid' markdown>

!!! failure "Error"

     ```html
	<Message messageContainerClassName="error" 
     messageContent="Secret key is required when sending session details is switched on, and should be at least 32 characters in length."/>
     ```

!!! success "Solution"

     This error can be resolved by filling in the `Session Details Signature Key` field or by disabling the `Send Studio signature header` field by selecting `No`.

</div>

#### Missing URL Error

>This message indicates that the REST API's URL field in the API editor form has been left empty.

<div class='grid' markdown>

!!! failure "Error"

     ```
	DEFAULT_REST_DATASOURCE is not correctly configured. Please fix the following and then re-run: \n[Missing URL.]
     ```

!!! success "Solution"

     This error can be fixed by editing the REST API form and providing a URL.

</div>

#### Missing Client Secret / Client ID / Access Token Error

>This message indicates that the mentioned parameter fields - `Client Secret`, `Client ID`, or  `Access Token URL` have been left empty. These fields are nested in the `Authentication` sub-section which becomes visible if the `Authentication Type` field has been chosen as OAuth 2.0.

<div class='grid' markdown>

!!! failure "Error"

     ```
     DEFAULT_REST_DATASOURCE is not correctly configured. Please fix the following and then re-run: \n[Missing Client Secret, Missing Client ID, Missing Access Token URL]
     ```

!!! success "Solution"

     This error can be fixed by filling in all the parameter fields.

</div>

#### Secret key required error

>This error message indicates that `Send Studio signature header` field has been marked as `Yes` but the `Session Details Signature Key` field is left empty.

<div class='grid' markdown>

!!! failure "Error"

     ```
     Secret key is required when sending session details is switched on, and should be at least 32 characters in length.
     ```

!!! success "Solution"

     This error can be resolved by filling in the `Session Details Signature Key` field or by disabling the `Send Studio signature header` field by selecting `No`.

</div>

## Git errors

Studio allows you to manage changes in your applications using git. The errors below may occur when your git setup is misconfigured or when collaborative editing introduces complexity.

### Common git errors

### Invalid Git repo

>This error message indicates that the SSH address provided is incorrect or access rules prevent connection to the repository.

<div class='grid' markdown>

!!! failure "Error"

     ```html
     <Message messageContainerClassName='error'
     messageContent='Invalid Git repo'></Message>
     ```

!!! success "Solution"

     Verify that the SSH address is correct and functional, check connection rules on the platform where the application is deployed, and if issues persist, contact support for assistance.

</div>

#### Invalid GitConfig

>This error message indicates that there is a Redis cache issue with user profiling, which causes an invalid Git configuration.

<div class='grid' markdown>

!!! failure "Error"

     ```html
     <Message messageContainerClassName='error'
     messageContent='Invalid Git repo'></Message>
     ```

!!! success "Solution"

     Logout from the application, and then login again to refresh the user profile and Git configuration. If issues persist, contact support for assistance.

</div>

#### Conflicts while merging

>This error message indicates that conflicts arose during the merging process when the same file has been edited on both branches. Git cannot automatically resolve these conflicts.

<div class='grid' markdown>

!!! failure "Error"

     ```html
     <Message messageContainerClassName='error'
     messageContent='Conflicts while merging branch b <= a'></Message>
     ```

!!! success "Solution"

     If you are facing conflicts in the Studio UI while merging branch `A` into branch `B`, raise a pull request targeting branch `B` on your Git provider, and manually resolve the conflicts. For more information, see [Resolve merge conflicts in Git](/version-control.md#resolve-merge-conflicts-in-git).

</div>

#### Git push failed for pending upstream changes

 >If you're working on branch `A` and someone else pushes changes to the remote counterpart of the same branch, you may encounter conflicts if both have edited the same files.

<div class='grid' markdown>

!!! failure "Error"

     ```html
     <Message messageContainerClassName='error'
     messageContent='Looks like there are pending upstream changes. To prevent you from losing history, we will pull the changes and push them to your repo.'></Message>
     ```

!!! success "Solution"

     Create a new branch from your local branch `A`, naming it branch `A-fix`. Raise a pull request from branch `A-fix` against the original branch `A`. Resolve conflicts within the pull request interface or locally before merging. In Studio, discard and pull the changes into branch `A`. For more information, see [Resolve merge conflicts in Git](/version-control.md#resolve-merge-conflicts-in-git).

</div>

#### Maximum call size exceeded error

>This error is due to the size limit on the merge operation being exceeded, possibly from large files or too many changes.

<div class='grid' markdown>

!!! failure "Error"

     ```html
     <Message messageContainerClassName='error'
     messageContent='Maximum call size exceeded'></Message>
     ```

!!! success "Solution"

     Split the merge operation into smaller chunks and remove any unnecessary large files from the repository.

</div>

#### Private repo limit error

>This error occurs due to restrictions on the number of private repositories that can be connected.

<div class='grid' markdown>

!!! failure "Error"

     ```html
     <Message messageContainerClassName='error'
     messageContent='Private Repo Limit Error'></Message>
     ```

!!! success "Solution"

     In Studio, you may only connect to three private repositories.

</div>

## JavaScript errors

While writing JavaScript in Studio, you may encounter the following errors in your code.

#### Reference errors

These occur when the code references an entity or variable that is not defined on the page. Review your bindings and the names of the entities to correct these errors.

#### Lint errors

Review the syntax of the mustache bindings for any syntax errors that could be causing issues. Javascript written inside mustache bindings can only be single line code. Use JSObjects for multi-line functions.

#### Type errors

Check your JavaScript operations to ensure you are not performing unsupported operations on certain data types.

### With debugger statement

To invoke the debugger, insert a `debugger` keyword in your code where you want it to pause, and then run your app. The code execution pauses on the debugger statement. It works like a `breakpoint`. You can then use the debugger tools to step through your code, inspect variables, and see how your code is executing.

**Syntax**

```
debugger;
```

**Example**:

```
export default {
    getUserDetails: async () => {
        const userInfo = await userDetailsAPI.run();
        debugger; // the execution is paused at this point
        console.log(“user information: “+userInfo); // The value of the userInfo
        variable is printed in the Logs tab.
        return userInfo;
    }
}
```

### With console.log()

In addition to using the debugger statement, you can use `console.log()` to print information about your code to the browser's console. This can help inspect the values of variables or the state of your app at different points during the execution of your code.

**Syntax**

```
console.log(<VARIABLE_NAME>);
```

# JS Errors
Errors may be encountered when using [JS Objects](/core-concepts/writing-code/javascript-editor-beta) or writing [JS functions](/core-concepts/writing-code/javascript-editor-beta/#types-of-js-functions). They can be caused by syntax errors in the code, data type mismatch, or attempts to access properties or functions that don't exist.


This section helps you troubleshoot common JS errors on the Appsmith platform.


## Data type evaluation errors


This error occurs when the value in the property of the widget doesn't match the data type required by the property.


#### Error message


<Message
messageContainerClassName="error"
messageContent="This value does not evaluate to type Array[Object]"></Message>




#### Cause


While working with [Tables](/reference/widgets/table/) or [Lists](/reference/widgets/list), you may encounter this error, as the data property expects an array of objects which might not match the data type of the API response.


#### Solution


The solution to this is to bind the array inside the response object or transform the response object using JavaScript. Take an example response of the fetch users API as below. Binding it to a [table](/reference/widgets/table/) directly would lead to an error.


```javascript
{
 "next": "https://mock-api.docs.spread.ai/users?page=2&pageSize=10",
 "previous": null,
 "users": [
   {
     "id": 1,
     "name": "Barty Crouch",
     "status": "APPROVED",
     "avatar": "https://robohash.org/sednecessitatibuset.png?size=100x100&set=set1",
     "email": "barty.crouch@gmail.com",
   },
   {
     "id": 2,
     "name": "Jenelle Kibbys",
     "status": "APPROVED",
     "avatar": "https://robohash.org/quiaasperiorespariatur.bmp?size=100x100&set=set1",
     "email": "jkibby1@hp.com",
   }
 ]
}
```


To overcome this, you can bind the user's array of the response instead of the entire response object using JavaScript:


```javascript
{{ '{{ fetch_users.data.users }}' }}
```
#### Error message


<Message
messageContainerClassName="error"
messageContent="This value does not evaluate to type Array[{`label: string, value: string`}]"></Message>




#### Cause


While adding options to single-select or multi-select dropdowns, you might face a data mismatch error. In such cases, make sure the `options` property is an array of objects containing a label and value as strings.


#### Solution


In case the response doesn't contain label and value keys as below, you can map over the response to transform it using JavaScript.


```javascript
// invalid response of fetchColors API
[
 'Blue',
 'Green',
 'Red'
]
```


```javascript
// Transform Response
{{ '{{ '{{ '{{
   fetchColors.data.map((color) =>{
       return {
           label: color,
           value: color
       }
   })
}}' }}
```
#### Error message


<Message
messageContainerClassName="error"
messageContent="The value does not evaluate to type Array [{x: string, y: number}]"></Message>


#### Cause


The below image shows that there is an error in the `Chart Data field` of the [Chart](/reference/widgets/chart) widget. The Evaluated Value here indicates the current value of the field, and in the screenshot below, you can see that the current value is an array while the error indicates that it must be an array\<x, y>.


![](/img/chart_error.png)


#### Solution


In cases like these, you can use JavaScript to transform the data to the correct data type or access the correct data inside the object. The below code reduces the fetch\_orders.data array to aggregate orders based on the date into an array \<x, y> where x is the date of the order and y is the order amount


```javascript
{{ '{{ '{{ '{{
   _.values(fetch_orders.data.reduce((accumulator, order) => {
       if(accumulator[order.date]) {
           accumulator[order.date].y += order.orderAmount
       } else {
           accumulator[order.date] = { x:order.date, y: order.orderAmount  };
       }
       return acc;
   }, {}))
}}' }}
```
#### Error message


<Message
messageContainerClassName="error"
messageContent="Value does not match ISO 8601 standard date string"></Message>


#### Cause


The date picker expects its default date in the standard [ISO format](https://www.iso.org/iso-8601-date-and-time-format.html). If the date you provided doesn't match this, you'll see this error.


#### Solution


To resolve this, you can transform the date string using moment.js.


```
// Moment can be used to set the default date to the current date
{{ '{{ '{{ '{{moment()}}' }}
```


```
// Moment can parse your date format
{{ '{{ moment("2021-07-26", "YYYY-MM-DD") }}' }}
```
#### Error message


<Message
messageContainerClassName="error"
messageContent="This value does not evaluate to type `boolean"></Message>




#### Cause
This error typically occurs in the `isVisible` and `isDisabled` properties and indicates that the value in the property doesn't match a `boolean` type.


#### Solution


You can solve this by using a comparison operator.


```
{{ '{{ Dropdown1.selectedOptionValue === "RED" }}' }}
```


#### Error message


<Message
messageContainerClassName="error"
messageContent="This value does not evaluate to type string"></Message>


#### Cause
When working with widgets, you may come across an error where the data property is expecting a string value that doesn't match the data type of the query response.


#### Solution


The solution to this issue is to convert the data type of the API response to a string. This can be done using JavaScript methods. Additionally, make sure that the data being passed to the widget is in the correct format. For example:


```
To get text,
{{ '{{ '{{ '{{Text1.text}}' }}


To get image,
{{ '{{ '{{ '{{Image1.image}}' }}
```


In case the preceding doesn't work, you can also check the EVALUATED VALUE section to make sure that it's returning a string value and not an object or other data type.


#### Error message

<Message
messageContainerClassName="error"
messageContent="This value must be number"></Message>


#### Cause
You may come across an error where the data property is expecting a numeric value that doesn't match the data type of the API response.


#### Solution


It's important to ensure that the data being passed to the widget's data property matches the expected data type. One solution to this issue is to use JavaScript to convert the API response to the correct data type, or to access the correct data type from the API response. 

You can also check the EVALUATED VALUE section to make sure that it's returning a numeric value and not an object or other data type.


## Syntax error


This error occurs when there is invalid JavaScript inside the handlebars `{{ '{{ }}' }}`. The evaluated value of the field is displayed as undefined in this case. Verify the number of braces in your code and consider re-writing your [JS as multi-line ](../../core-concepts/writing-code/#multi-line-javascript)code.


In the example below, fetch isn't defined anywhere in the application


![](/img/syntax_error.png)




## Cyclic dependency error


An app gets a cyclic dependency error when a node is directly or indirectly dependent on itself.


#### Reactivity and dependency map


In Appsmith, all user-editable fields are defined as nodes, and to provide reactivity, a dependency map is created between these nodes to find the optimal evaluation order of these nodes. For example, when you would refer to `{{ '{{ '{{ '{{Api1.data}}' }}` in a Table1's `tableData` field, there is a dependency created between `Api1.data` and `Table1.tableData`. So every time `Api1.data` updates, `Table1.tableData` needs to be updated.


```
// Table1.tableData depends on Api1.data
Api1.data -> Table1.tableData
```


Similarly, all parent nodes are implicitly dependent on the child nodes to ensure updates are propagated up an entity object. A more straightforward way to understand this is that if a child node updates, the parent node, and its dependencies should also be updated.


```
// Implicit. Parent depends on children
Api1.data -> Api1
Table1.tableData -> Table1


// Explicit. Table1.tableData depends on Api1.data
Api1.data -> Table1.tableData
```


The most common scenario where a cycle occurs is when you would try to bind a node to its parent node. Since it's impossible to evaluate an app with a cyclic dependency, you have to exit out and be in an error state till the cycle is resolved.


```
// A cycle is formed
Table1 -> Table1.tableData
Table1.isVisible -> Table1
```


## Infinite loop error
An infinite loop error occurs when a function or code block repeats indefinitely, causing the app or function to become unresponsive, and can even prevent users from accessing certain features of the app.
#### Cause
The problem may be due to a page load function that's stuck in a loop. This can happen if you have added code that uses the `navigateTo` function and is executed on `onPageLoad`, which can cause the page to become inaccessible or cause the app to get stuck in a loop and constantly routing to the destination page.


#### Solution
To fix this problem, you can use debugger statements in Appsmith to halt the execution of the code and identify the source of the infinite loop. Here are the steps to do this:


1. Open the app in Appsmith and go to the page where the infinite loop is occurring.
2. Locate the function or code block that's causing the infinite loop.
3. Insert a debugger statement at the beginning of the function or code block that pauses the execution of the code and allows you to inspect its state. For more information, see [debugging statement and how to use it](/core-concepts/writing-code/javascript-editor-beta/#debugger-statements).
4. Use the debugger console of the browser to step through the code and identify the cause of the infinite loop.
5. Once you have identified the issue, make the necessary changes to the code to fix it.
6. Save the changes and test the app again to ensure the infinite loop issue has been resolved.


If you can't find what you are looking for and need help debugging an error, please raise your issue on [Discord Server](https://discord.com/invite/rBTTVJp) or email at support@docs.spread.ai.



