# Getting Started with the Kosha SDK in Javascript

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

1. Install the dependencies by changing into the extracted directory containing `package.json` i.e., the javascript-client

For a specific user:
```sh
  cd javascript-client
  npm install
```

Finally, build the module:

```sh
npm run build
```

This will create a `dist` folder inside `javascript-client` containing the bundle which we can import and use within our client app.

##### Import and Configure

```javascript
var ConnectorApi = require('./dist');

// this will be your deployed connector url
var opts = {
  'basePath': 'https://connector.your-org.kosha',
};

var a = new ConnectorApi.ApiClient(opts.basePath);

// add your kosha jwt token as a header
a.defaultHeaders = {
  "Authorization": "Bearer " + "<your-kosha-jwt-token>"
};

// e.g., we are interested in PeopleApi class
var api = new ConnectorApi.PeopleApi(a);

var callback = function(error, data, response) {
  if (error) {
    console.error(error);
  } else {
    console.log('API called successfully. Returned data: ');
    console.log(data);
  }
};
// e.g., endpoint is /api/v1/me under PeopleApi
console.log(api.apiV1MeGet(callback));
```

