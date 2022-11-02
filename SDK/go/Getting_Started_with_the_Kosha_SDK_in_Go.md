# Getting Started with the Kosha SDK in Go


##### What you'll learn
- [x] How to interact with the Kosha user interface to obtain the client library in Golang
- [x] How to add the Kosha client library to your project
- [x] How to programatically connect to a Kosha endpoint using the client SDK 

## Installation

##### Download the SDK
1. Navigate to **My Connectors** in the Connectors tab and click into your connector of choice.
2. Click into Usage & SDK
3. You should see this screen with a variety of language options presented. 
![image info](../images/usage_sdk.png)
4. Click on Go and select the option to download its SDK.
![image info](../images/download_sdk.png)

##### Install Into Project
1. Unzip the Go SDK into your project 
```sh
tar -xvf <generated_client>.zip -C <your_project_directory>
```

**_NOTE:_** There is no need to modify code in the client library.

2. Download all go client dependencies


```sh
go mod tidy
go mod download
```

##### Import and Configure

```go
package main

import (
	"fmt"
	"github.com/kosha/go-sdk/openapi"
)

func main() {
	cfg := &openapi.Configuration{
		DefaultHeader: make(map[string]string),
		UserAgent:     "OpenAPI-Generator/1.0.0/go",
		Servers: openapi.ServerConfigurations{
			{
				URL:         "https://<your_connector_name>.<your_company>.dev.kosha.app",
				Description: "No description provided",
			},
		},
		OperationServers: map[string]openapi.ServerConfigurations{},
	}

	client := openapi.NewAPIClient(cfg)
	res := openapi.<endpoint>{
		ApiService: client.<your-api-service>,
	}
	_, response, err := res.Execute()
	if err != nil {
		fmt.Println("error: %v", err)
	}
	fmt.Println(response)
}

```
