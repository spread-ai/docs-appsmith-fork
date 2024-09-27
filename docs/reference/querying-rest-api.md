---
description: Query a REST API from Appsmith.
---

# REST API

This page describes how to connect your application to a REST API and use queries to read and write data in your applications.

Use this datasource to create a single query for an API that doesn't need complex authentication settings. If you plan to create multiple queries for the same API, you may want to use an [Authenticated API](/connect-data/reference/authenticated-api) datasource. Every query created from an Authenticated API datasource shares configuration (root URL, authentication, headers, and so on) to avoid re-entering details.

## Query REST API

The following section is a reference guide that provides a description of the parameters to create REST API queries.

<ZoomImage src="/img/restapi-query-config.png" alt="Configuring a REST API query." caption="Configuring a REST API query." />

#### Method

 Sets the REST method (<code>GET</code>, <code>POST</code>, etc.) to use for the request.

#### URL

 Sets the endpoint to query.

#### Headers

 Sets key/value pairs to send in the request header.
 <em>To learn how to set up dynamic headers, visit and fork this <a href="https://app.appsmith.com/applications/6200ac292cd3d95ca414dc4f/pages/624eda0551a8863d6c406760">sample app</a></em>.

#### Params

 Sets key/value pairs to send as query parameters in the request.

#### Body

 
Appsmith supports a variety of encoding types for sending data in API queries. The encoding type can be selected via the Body dropdown on the API editor. For step-by-step instructions on uploading files using an API, see <a href="/build-apps/how-to-guides/Send-Filepicker-Data-with-API-Requests">Upload Files using API</a> guide.<br/>

 
  <i>Options:</i>
  <ul>
    <li><b>None:</b> Omits a body from the request.</li>
    <li><b>JSON:</b> Expects a JSON object to send as the body.</li>
  </ul>
 
  <pre>
    {` 
      {
        "q": {{ '{{ UsersTable.searchText }}' }},
        "limit": {{ '{{ UsersTable.pageSize }}' }},
        "offset": {{ '{{ UsersTable.pageOffset }}' }}
      }
    `}
  </pre>
  In the example above, values are collected from a Table widget and passed into a JSON object.

  <ul>
    <li><b>FORM_URLENCODED:</b> Expects key/value pairs to be encoded into FORM_URLENCODED format as the body.</li>
  </ul>

 

  | Key    | Value                         |
  | ------ | ----------------------------- |
  | query  | `{{ '{{ UsersTable.searchText }}' }}` |
  | limit  | `{{ '{{ UsersTable.pageSize }}' }}`   |
  | offset | `{{ '{{ UsersTable.pageOffset }}' }}` |

  <pre>{`// result
  "query=arjun&limit=10&offset=20"
  `}</pre>
  <p>Selecting <b>FORM_URLENCODED</b> (for <code>application/x-www-form-urlencoded</code>) automatically encodes your key/value pairs for sending in the request body.</p>

<ul>
  <li><b>MULTIPART_FORM_DATA:</b> Expects key/value pairs with a data type to be encoded into MULTIPART_FORM_DATA format as the body. Multipart requests can include several different types of data within them, such as a file along with some other related metadata.</li>
</ul>
 

| Key      | Type | Value                       |
| -------- | ---- | --------------------------- |
| user     | Text | `{{ '{{ appsmith.user.email }}' }}` |
| filename | Text | `{{ '{{ FileNameInput.text }}' }}`  |
| file     | File | `{{ '{{ Filepicker.files[0] }}' }}` |

<pre>{`// result
"query=arjun&limit=10&offset=20"
`}</pre>
<p>Above, values of multiple types are pulled from widgets and added to the query, including file data from a <a href="/reference/widgets/filepicker">Filepicker widget</a>.</p>

tip
When uploading file data, check that your Filepicker widget's **Data Format** property is set correctly. When uploading as multipart/form-data, this should usually be set to `Binary`.



<ul>
  <li><b>BINARY:</b> For any Base64 upload, including text files, images, videos, and more, ensure that you include the file data in the body. If you're using Binary to upload files, remember to set the [Data Format](/reference/widgets/filepicker#data-format-string) property of the Filepicker widget to `Base64`. This ensures that the file data is encoded correctly before transmission. Moreover, if the API you are connecting with expects additional key/value pairs, you can include them along with file data in the body.</li>
</ul>
 
<pre>`{{ '{{ imgFilepicker.files[0].data }}' }}`</pre>
<p>In the above example, if the API expects to supply only the image data, use the `data` property of the Filepicker widget to send the data of the selected image file.</p>


<ul>
  <li><b>RAW:</b> Expects raw binary file data to be sent as the body.</li>
</ul>
   <pre>{`{{ '{{ Filepicker1.files[0]?.data }}' }}
`}</pre>
<p>Use <b>RAW</b> if your endpoint can't accept multipart-encoded data and requires raw body binary instead. Above, the <code>data</code> property of the file is passed to the query instead of the file object itself because the endpoint expects only raw binary data.</p>

caution tip
Be sure to turn off **JSON Smart Substitution** for this query in the [query settings](/connect-data/reference/query-settings). This option usually helps cast data into correct JSON, but it is problematic when used with RAW binary.






#### Pagination

 
  <i>Options:</i>
  <ul>
    <li><b>None:</b> Doesn't use any pagination.</li>
    <li><b>Paginate with Table Page No:</b> Use when your API expects an offset or increment value to determine which set of records to return. Follow the instructions that appear on the platform, or see <a href="/build-apps/how-to-guides/Server-side-pagination-in-table">Offset-based pagination</a> for more information.</li>
    <li><b>Paginate with Response URL:</b> Use when your API returns cursor values to page through data. The <b>Previous URL</b> and <b>Next URL</b> fields expect the cursor values from the query response. For more information, see <a href="/build-apps/how-to-guides/Server-side-pagination-in-table">Cursor-based pagination</a>.</li>
  </ul>


#### Authentication

 <em>Click the button in this tab to turn this query into a new Authenticated API datasource where you can configure Authentication for your requests.</em>

## Troubleshooting

If you're experiencing difficulties, you can refer to to the [Datasource troubleshooting guide](/help-and-support/troubleshooting-guide/action-errors/datasource-errors), or contact the support team using the chat widget at the bottom right of this page.



# Fetch API
The Fetch API provides an interface for executing network calls programmatically. You can use `fetch()` to programmatically configure and execute a REST API.  

**Examples**

**GET request**

Fetches data from the specified URL using a GET request and parses the JSON response.

```javascript
const questions = await fetch("https://opentdb.com/api.php?amount=10")
return questions.json()
```

**POST request**

Sends a POST request to create a new resource with the provided data and logs the success or error.

```javascript
fetch("https://63772c9a5c477765121615ba.mockapi.io/users", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
  },
  body: JSON.stringify({
    name: "Alex",
    email: "alex@appsmith.com",
  }),
}).then((response) => {
    console.log("Success:", response.json());
}).catch((error) => {
    console.error("Error:", error);
});
```


**PUT request**

The PUT method in the Fetch API is used to update a resource on the server. It is typically used when you want to update the entire resource or create it if it doesn't exist. Here's an example of how you can use the PUT method with the Fetch API:

```js
fetch("https://63772c9a5c477765121615ba.mockapi.io/users/1", {
  method: "PUT",
  headers: {
    "Content-Type": "application/json",
  },
  body: JSON.stringify({
    name: "UpdatedName",
    email: "updated_email@example.com",
  }),
})
  .then((response) => {
    if (!response.ok) {
      throw new Error(`HTTP error! Status: ${response.status}`);
    }
    return response.json();
  })
  .then((data) => {
    console.log("Success:", data);
  })
  .catch((error) => {
    console.error("Error:", error);
  });
```

**File upload**

Uploads a file using a POST request with a FormData object and logs the response.


```javascript
const formData = new FormData();
formData.append("file", FilePicker1.files[0]);
		
let response = await fetch('https://httpbin.org/post', {
	method: 'POST',
	body: formData
});
```