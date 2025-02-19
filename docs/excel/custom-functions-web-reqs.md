---
ms.date: 06/21/2019
description: Request, stream, and cancel streaming of external data to your workbook with custom functions in Excel
title: Receive and handle data with custom functions
localization_priority: Priority
---

# Receive and handle data with custom functions

One of the ways that custom functions enhances Excel's power is by receiving data from locations other than the workbook, such as the web or a server (through WebSockets). Custom functions can request data through XHR and `fetch` requests as well as stream this data in real time.

[!include[Excel custom functions note](../includes/excel-custom-functions-note.md)]

The documentation below illustrates some samples of web requests, but to build a streaming function for yourself, try the [Custom functions tutorial](../tutorials/excel-tutorial-create-custom-functions.md).

## Functions that return data from external sources

If a custom function retrieves data from an external source such as the web, it must:

1. Return a JavaScript Promise to Excel.
2. Resolve the Promise with the final value using the callback function.

You can request external data through an API like [`Fetch`](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) or by using `XmlHttpRequest` [(XHR)](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest), a standard web API that issues HTTP requests to interact with servers.

Within custom functions runtime, XHR implements additional security measures by requiring [Same Origin Policy](https://developer.mozilla.org/en-US/docs/Web/Security/Same-origin_policy) and simple [CORS](https://www.w3.org/TR/cors/).

Note that a simple CORS implementation cannot use cookies and only supports simple methods (GET, HEAD, POST). Simple CORS accepts simple headers with field names `Accept`, `Accept-Language`, `Content-Language`. You can also use a Content-Type header in simple CORS, provided that the content type is `application/x-www-form-urlencoded`, `text/plain`, or `multipart/form-data`.

### XHR example

In the following code sample, the **getTemperature** function calls the sendWebRequest function to get the temperature of a particular area based on thermometer ID. The sendWebRequest function uses XHR to issue a GET request to an endpoint that can provide the data.

```js
/**
 * Receives a temperature from an online source.
 * @customfunction
 * @param {number} thermometerID Identification number of the thermometer.
 */
function getTemperature(thermometerID) {
  return new Promise(function(setResult) {
      sendWebRequest(thermometerID, function(data){
          storeLastTemperature(thermometerID, data.temperature);
          setResult(data.temperature);
      });
  });
}

// Helper method that uses Office's implementation of XMLHttpRequest in the JavaScript runtime for custom functions.  
function sendWebRequest(thermometerID, data) {
    var xhttp = new XMLHttpRequest();
    xhttp.onreadystatechange = function() {
        if (this.readyState == 4 && this.status == 200) {
           data.temperature = JSON.parse(xhttp.responseText).temperature
        };

        //set Content-Type to application/text. Application/json is not currently supported with Simple CORS
        xhttp.setRequestHeader("Content-Type", "application/text");
        xhttp.open("GET", "https://contoso.com/temperature/" + thermometerID), true)
        xhttp.send();  
    }
}

CustomFunctions.associate("GETTEMPERATURE", getTemperature);
```

For another sample of an XHR request with more context, see the `getFile` function within [this file](https://github.com/OfficeDev/Office-Add-in-JavaScript-FileDownload/blob/master/FileDownloadSampleWeb/Home.js) in the [Office-Add-in-JavaScript-FileDownload](https://github.com/OfficeDev/Office-Add-in-JavaScript-FileDownload) Github repository.

### Fetch example

In the following code sample, the `stockPriceStream` function uses a stock ticker symbol to get the price of a stock every 1000 milliseconds. For more details about this sample, see the [Custom functions tutorial](../tutorials/excel-tutorial-create-custom-functions.md#create-a-streaming-asynchronous-custom-function).

> [!NOTE]
> The following code requests a stock quote using the IEX Trading API. Before you can run the code, you'll need to [create a free account with IEX Cloud](https://iexcloud.io/) so that you can get the API token that's required in the API request.

```js
/**
 * Streams a stock price.
 * @customfunction 
 * @param {string} ticker Stock ticker.
 * @param {CustomFunctions.StreamingInvocation<number>} invocation Invocation parameter necessary for streaming functions.
 */
function stockPriceStream(ticker, invocation) {
    var updateFrequency = 1000 /* milliseconds*/;
    var isPending = false;

    var timer = setInterval(function() {
        // If there is already a pending request, skip this iteration:
        if (isPending) {
            return;
        }

        //Note: In the following line, replace <YOUR_TOKEN_HERE> with the API token that you've obtained through your IEX Cloud account.
        var url = "https://cloud.iexapis.com/stable/stock/" + ticker + "/quote/latestPrice?token=<YOUR_TOKEN_HERE>"
        isPending = true;

        fetch(url)
            .then(function(response) {
                return response.text();
            })
            .then(function(text) {
                invocation.setResult(parseFloat(text));
            })
            .catch(function(error) {
                invocation.setResult(error);
            })
            .then(function() {
                isPending = false;
            });
    }, updateFrequency);

    invocation.onCanceled = () => {
        clearInterval(timer);
    };
}

CustomFunctions.associate("STOCKPRICESTREAM", stockPriceStream);
```

## Receive data via WebSockets

Within a custom function, you can use WebSockets to exchange data over a persistent connection with a server. By using WebSockets, your custom function can open a connection with a server and then automatically receive messages from the server when certain events occur, without having to explicitly poll the server for data.

### WebSockets example

The following code sample establishes a WebSocket connection and then logs each incoming message from the server.

```js
let ws = new WebSocket('wss://bundles.office.com');

ws.onmessage(message) {
    console.log(`Received: ${message}`);
}

ws.onerror(error){
    console.err(`Failed: ${error}`);
}
```

## Make a streaming function

Streaming custom functions enable you to output data to cells that updates repeatedly, without requiring a user to explicitly refresh anything. This can be useful to check live data from a service online, like the function in [the custom functions tutorial](../tutorials/excel-tutorial-create-custom-functions.md).

To declare a streaming function, use the JSDoc comment tag `@stream`. To alert users to the fact that your function may re-evaluate based on new information, consider putting stream or other wording to indicate this in the name or description of your function.

The following example shows a streaming function which increases a given number every second by an amount you specify.

```JS
/**
 * Increments a value once a second.
 * @customfunction INC increment
 * @param {number} incrementBy Amount to increment
 * @param {CustomFunctions.StreamingInvocation<number>} invocation
 */
function increment(incrementBy, invocation) {
  let result = 0;
  const timer = setInterval(() => {
    result += incrementBy;
    invocation.setResult(result);
  }, 1000);

  invocation.onCanceled = () => {
    clearInterval(timer);
  };
}
CustomFunctions.associate("INC", increment);
```

>[!NOTE]
> Note that there are also a category of functions called cancelable functions, which are *not* related to streaming functions. Previous versions of custom functions required you to declare `"cancelable": true` and `"streaming": true` in JSON written by hand. Since the introduction of autogenerated metadata, only asynchronous custom functions which return one value are cancelable. Cancelable functions allow a web request to be terminated in the middle of a request, using a [`CancelableInvocation`](/javascript/api/custom-functions-runtime/customfunctions.cancelableinvocation) to decide what to do upon cancellation. Declare a cancelable function using the tag `@cancelable`.

### Using an invocation parameter

The `invocation` parameter is the last parameter of any custom function by default. The `invocation` parameter gives context about the cell (such as its address) and also allows you to use `setResult` and `onCanceled` methods. These methods define what a function does when the function streams (`setResult`) or is canceled (`onCanceled`).

If you're using TypeScript, the invocation handler needs to be of type `CustomFunctions.StreamingInvocation` or `CustomFunctions.CancelableInvocation`.

### Streaming and cancelable function example
The following code sample is a custom function that adds a number to the result every second. Note the following about this code:

- Excel displays each new value automatically using the `setResult` method.
- The second input parameter, invocation, is not displayed to end users in Excel when they select the function from the autocomplete menu.
- The `onCanceled` callback defines the function that executes when the function is canceled.

```js
/**
 * Increments a value once a second.
 * @customfunction
 * @param {number} incrementBy Amount to increment.
 * @param {CustomFunctions.StreamingInvocation<number>} invocation Invocation parameter necessary for streaming functions.
 */
function increment(incrementBy, invocation) {
  let result = 0;
  const timer = setInterval(() => {
    result += incrementBy;
    invocation.setResult(result);
  }, 1000);

  invocation.onCanceled = function(){
    clearInterval(timer);
    }
}
CustomFunctions.associate("INCREMENT", increment);
```

>[!NOTE]
> Excel cancels the execution of a function in the following situations:
>
> - When the user edits or deletes a cell that references the function.
> - When one of the arguments (inputs) for the function changes. In this case, a new function call is triggered following the cancellation.
> - When the user triggers recalculation manually. In this case, a new function call is triggered following the cancellation.

## Next steps

* Learn about [different parameter types your functions can use](custom-functions-parameter-options.md).
* Discover how to [batch multiple API calls](custom-functions-batching.md).

## See also

* [Volatile values in functions](custom-functions-volatile.md)
* [Create JSON metadata for custom functions](custom-functions-json-autogeneration.md)
* [Custom functions metadata](custom-functions-json.md)
* [Runtime for Excel custom functions](custom-functions-runtime.md)
* [Custom functions best practices](custom-functions-best-practices.md)
* [Create custom functions in Excel](custom-functions-overview.md)
* [Excel custom functions tutorial](../tutorials/excel-tutorial-create-custom-functions.md)
