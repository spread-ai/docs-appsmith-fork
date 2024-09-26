---
title: Connecting to a GraphQL data source
description: Connect Studio to a GraphQL API and create queries.
---

This page provides information for connecting your application to a GraphQL API and for using queries to manage its content.

## Create queries

The following section is a reference guide that provides a complete description of all the read and write operation commands with their parameters to create GraphQL queries.

<ZoomImage
  src="/img/graphql-query-config.png" 
  alt="Create a GraphQL query."
  caption="Create a GraphQL query."
/>

GraphQL queries are written in the **Body** tab of the query screen. Use the **Query** window to construct your query or mutation, and the adjacent **Query Variables** window to add any variables to map into your query.

### Fetch records

Use a query like the one below to retrieve records from your datasource.

In the example below, `UsersTable` is the name of a Table widget used to search for a user by name and display the results. This query uses `limit` and `offset` to implement [**server-side pagination**](/build-apps/how-to-guides/Server-side-pagination-in-table).

In the **Query** window:

```javascript
query GetUserData ($name: String!, $limit: Int!, $offset: Int!) {
  user (name: $name, first: $first, offset: $offset) {
    id
    name
    email
    date_of_birth
  }
}
```

In the **Query variables** window:

```javascript
{
  "name": {{ '{{ UsersTable.searchText }}' }},
  "limit": {{ '{{ UsersTable.pageSize }}' }},
  "offset": {{ '{{ UsersTable.pageOffset }}' }}
}
```

### Insert a record

Use an insert mutation to add new records to your GraphQL datasource.

In the example below, `CreateUserForm` is the name of a [Form widget](/reference/widgets/form) used to collect input for the new record.

In the **Query** window:

```javascript
mutation CreateUser (name: String!, email: String!, date_of_birth: String!){
  createUser(name: $name, email: $email, date_of_birth: $date_of_birth) {
    id
    name
    email
    date_of_birth
  }
}
```

In the **Query variables** window:

```javascript
{
  "name": {{ '{{ CreateUserForm.data.name }}' }},
  "email": {{ '{{ CreateUserForm.data.email }}' }},
  "date_of_birth": {{ '{{ CreateUserForm.data.date_of_birth }}' }}
}
```

### Update a record

Use an update mutation to modify an existing record in your dataset.

In the example below, `UpdateUserForm` is the name of a [Form widget](/reference/widgets/form) used to collect input for the new record.

In the **Query** window:

```javascript
mutation UpdateUser (id: Int!, name: String, email: String, date_of_birth: String){
  updateUser(id: $id, name: $name, email: $email, date_of_birth: $date_of_birth) {
    id
    name
    email
    date_of_birth
  }
}
```

In the **Query variables** window:

```javascript
{
  "id": {{ '{{ UpdateUserForm.data.id }}' }}
  "name": {{ '{{ UpdateUserForm.data.name }}' }},
  "email": {{ '{{ UpdateUserForm.data.email }}' }},
  "date_of_birth": {{ '{{ UpdateUserForm.data.date_of_birth }}' }}
}
```

### ​Delete a record​

Use a delete mutation to delete an existing record from your dataset.

In the example below, `UsersTable` is the name of a Table widget used to display the results from a previous query.

In the **Query** window:

```javascript
mutation DeleteUser (id: Int!){
  deleteUser(id: $id) {
    id
    name
    email
    date_of_birth
  }
}
```

In the **Query variables** window:

```javascript
{
  "id": {{ '{{ UpdateUserForm.data.id }}' }}
}
```




## Connection parameters

Authenticated GraphQL API datasources share configuration fields with the Authenticated API datasource. For a reference guide of the fields for configuring your Authenticated GraphQL API, see [Authenticated API](/connect-data/reference/authenticated-api).

<ZoomImage
  src="/img/graphql-datasource-config.png" 
  alt="Configure a GraphQL datasource"
  caption="Configure a GraphQL datasource"
/>

## Connection parameters

The following section provides a detailed view of essential as well as optional parameters to establish a connection with an API datasource.

<ZoomImage src="/img/restapi-datasource-config.png" alt="Configuring an Authenticated API datasource" caption="Configuring an Authenticated API datasource" />

:::caution
The datasource configuration fields do not accept JavaScript code or bindings using mustache `{{ '{{}}' }}` syntax.
:::

### URL

 

The uniform resource locator (URL) specifies the address of the service or endpoint to which the requests will be made. This is typically the base URL of the REST API you are connecting to. If you wish to connect to a local database or API, see the [Connect Local Datasource](/connect-data/how-to-guides/how-to-work-with-local-apis-on-appsmith) guide.




### Send Appsmith signature header

 
When enabled, Appsmith adds an extra header, `X-Appsmith-Signature`, to your requests. This header contains a JSON Web Token (JWT) signed with a secret string. You can use this header to verify that the incoming requests are originating from Appsmith. This mechanism ensures the integrity and authenticity of requests originating from Appsmith.


### Use self-signed certificate

 
When enabled, this option allows you to upload a self-signed certificate in the .PEM (Privacy Enhanced Mail) format, which is securely stored in an encrypted format. This certificate is then included in the request made by Appsmith to the endpoint.


### Headers

 

Headers contain key-value pairs that you include in the header section of your HTTP requests. You use headers to provide information to the server, such as authentication tokens, content types, or custom headers required by the API you are connecting to.



### Query parameters

 
Query parameters consist of key-value pairs passed as parameters in the URL of your HTTP requests. You use query parameters to provide specific information to the server, such as filtering criteria, sorting options, or specific data needed for the request.



### Authentication type

 
The authentication type setting determines the method used to authenticate requests. You can configure the details under the Authentication dropdown menu. The available options are:
  - **None**- When selected, Appsmith doesn't send authentication information with the request. Use this option if your API doesn't require authentication details in the request.  
  - **Basic**- When selected, Appsmith sends the Username and Password in the Authorization header of each request as a base64-encoded string. Use this option if your API requires username and password details in the request.
  - **OAuth 2.0**- When selected, Appsmith enables integration with APIs that require OAuth 2.0 authentication. With OAuth 2.0 you can configure secure authorization flows, allowing you to grant limited access to resources. For more information, see the [OAuth 2.0 Configuration](#oauth-20) section.
  - **API Key**- When selected, Appsmith sends a key-value pair in the Authorization header of each request. This method is commonly used for API authentication, where the API hosting provider supplies a unique API key to the client for securely accessing the APIs.
  - **Bearer Token**- When selected, Appsmith sends a bearer token value in the Authorization header of each request. This method is commonly used for token-based authentication, where the API hosting provider supplies a token to the client for securely accessing the APIs.



