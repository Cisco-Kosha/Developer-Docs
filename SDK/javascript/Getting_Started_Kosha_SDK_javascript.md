# Getting Started with the Kosha SDK in JavaScript

Kosha provides you with a SDK in a variety of languages to get your connectors integrated into your code and processes with minimal toil. Each connector has its own SDK as a collection of client libraries for the connector API. Using this SDK will allow for faster development and cleaner code.  

##### What you'll learn
- [x] How to interact with the Kosha user interface to obtain the client library
- [x] How to add the Kosha client library to your project
- [x] How to programatically connect to a Kosha endpoint using the client SDK 

## Installation

##### Download the SDK
1. Navigate to **My Connectors** in the Connectors tab and click into your connector of choice.
2. Click into Usage & SDK
3. You should see this screen with a variety of language options presented. 
![image info](../images/usage_sdk.png)
4. Click into your language of choice and select the option to download its SDK.
![image info](../images/download_sdk.png)

##### Install Into Project
1. Unzip the SDK into your project 
```sh
tar -xvf <generated_client>.zip -C <your_project_directory>
```

**_NOTE:_** There is no need to modify code in the client library.

2. Install into pip via the Setuptools based setup.py script

For a specific user:
```sh
npm install
```
For all users:
```sh
node ./main.js or npm run start
```

##### Import and Configure

```javascript with go-sdk
// so we will define our constants here
const openapi-kosha = require("openapi-client");

const url = '"https://<your_connector_name>.<your_company>.dev.kosha.app/<your_endpoint_path>"';

const data = {} // modify as per the request

openapi-kosha.init({
  url: url, // set your service url explicitly. Defaults to the one generated from your OpenAPI spec
  getAuthorization // Add a `getAuthorization` handler for when a request requires auth credentials
});
 
// The param 'security' represents the security definition in your OpenAPI spec a request is requiring
// For bearer type it has two properties:
// 1. id - the name of the security definition from your OpenAPI spec
// 2. scopes - the token scope(s) required
// Should return a promise
function getAuthorization(security) {
  switch (security.id) {
    case 'account': return getAccountToken(security);
    // case 'api_key': return getApiKey(security); // Or any other securityDefinitions from your OpenAPI spec
    default: throw new Error(`Unknown security type '${security.id}'`)
  }
};

function getAccountToken(security) {
  const token = findAccountToken(security); // A utility function elsewhere in your application that returns a string containing your token – possibly from Redux or localStorage
  if (token) return Promise.resolve({ token: token.value });
  else throw new Error(`Token ${type} ${security.scopes} not available`);
}
// now we configure the fetch request to the url endpoint.
// we should probably put it inside a separate function since
// you're using a browser, you probably will bind this request
// to a click event or something.
function makeRequest() {
  return fetch(url, {
    // in the case of a login request most APIs use the POST method offered by
    // RESTful APIs
    method: 'post', // can be 'get', 'put', 'delete', and many more

    // now we set any needed headers specified by the API
    headers: {
      // most APIs I have worked with use
      'Content-Type': 'application/json',
      // but some might need more, they will specify anyway.
    },

    // because we are using the 'post' method then we will need to add
    // a body to the request with all our data, body excepts a string so
    // we do the following
    body: JSON.stringify({
        data  
    }),
  })
  // Now we handle the response because the function returns a promise
  .then((response) => {
    // An important thing to note is that an error response will not throw
    // an error so if the result is not okay we should throw the error
    if(!response.ok) {
      throw response;
    }

    // since we expect a json response we will return a json call
    return response.json();
  })
}

````

### The world is your oyster!
Now that you've implemented one endpoint for one connector, you can implement any other endpoint in any other connector within Kosha. The process is universal across connectors and allows for clean, consistent code across your applications.

