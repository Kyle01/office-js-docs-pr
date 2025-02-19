---
ms.date: 06/21/2019
description: Troubleshoot common problems in Excel custom functions.
title: Troubleshoot custom functions
localization_priority: Priority
---
# Troubleshoot custom functions

When developing custom functions, you may encounter errors in the product while creating and testing your functions.

[!include[Excel custom functions note](../includes/excel-custom-functions-note.md)]

To resolve issues, you can [enable runtime logging to capture errors](#enable-runtime-logging) and refer to [Excel's native error messages](#check-for-excel-error-messages). Also, check for common mistakes such as [leaving promises unresolved](#ensure-promises-return) and forgetting to [associate your functions](#my-functions-wont-load-associate-functions).

## Enable runtime logging

If you are testing your add-in in Office on Windows, you should [enable runtime logging](/office/dev/add-ins/testing/troubleshoot-manifest#use-runtime-logging-to-debug-your-add-in). Runtime logging delivers `console.log` statements to a separate log file you create to help you uncover issues. The statements cover a variety of errors, including errors pertaining to your add-in's XML manifest file, runtime conditions, or installation of your custom functions.  For more information about runtime logging, see [Use runtime logging to debug your add-in](/office/dev/add-ins/testing/troubleshoot-manifest#use-runtime-logging-to-debug-your-add-in).  

### Check for Excel error messages

Excel has a number of built-in error messages which are returned to a cell if there is calculation error. Custom functions only use the following error messages: `#NULL!`, `#DIV/0!`, `#VALUE!`, `#REF!`, `#NAME?`, `#NUM!`, `#N/A`, and `#BUSY!`.

Generally, these errors correspond to the errors you might already be familiar with in Excel. The are only a few exceptions specific to custom functions, listed here:

- A `#NAME` error generally means there has been an issue registering your functions.
- A `#VALUE` error typically indicates an error in the functions' script file.
- A `#N/A` error is also maybe a sign that that function while registered could not be run. This is typically due to a missing `CustomFunctions.associate` command.
- A `#REF!` error may indicate that your function name is the same as a function name in an add-in that already exists.

## Clear the Office cache

Information about custom functions is cached by Office. Sometimes while developing and repeatedly reloading an add-in with custom functions your changes may not appear. You can fix this by clearing the Office cache. For more information, see the "Clear the Office cache" section in the article [Validate and troubleshoot issues with your manifest](https://docs.microsoft.com/office/dev/add-ins/testing/troubleshoot-manifest?branch=master#clear-the-office-cache)

## Common issues

### My functions won't load: associate functions

In your custom functions' script file, you need to associate each custom function with its ID specified in the [JSON metadata file](custom-functions-json.md). This is done by using the `CustomFunctions.associate()` method. Typically this method call is made after each function or at the end of the script file. If a custom function is not associated, it will not work.

The following example shows an add function, followed by the function's name `add` being associated with the corresponding JSON id `ADD`.

```js
/**
 * Add two numbers.
 * @customfunction
 * @param {number} first First number.
 * @param {number} second Second number.
 * @returns {number} The sum of the two numbers.
 */
function add(first, second) {
  return first + second;
}

CustomFunctions.associate("ADD", add);
```

For more information on this process, see [Associating function names with json metadata](/office/dev/add-ins/excel/custom-functions-best-practices#associating-function-names-with-json-metadata).

### Can't open add-in from localhost: use a local loopback exception

If you see the error "We can't open this add-in from localhost," you will need to enable a local loopback exception. For details on how to do this, see [this Microsoft support article](https://support.microsoft.com/en-us/help/4490419/local-loopback-exemption-does-not-work).

### Runtime logging reports "TypeError: Network request failed" on Excel on Windows

If you see the error "TypeError: Network request failed" in your [runtime log](custom-functions-troubleshooting.md#enable-runtime-logging) while making calls to your localhost server, you'll need to enable a local loopback exception. For details on how to do this, see *Option #2* in [this Microsoft support article](https://support.microsoft.com/en-us/help/4490419/local-loopback-exemption-does-not-work).

### Ensure promises return

When Excel is waiting for a custom function to complete, it displays #BUSY! in the cell. If your custom function code returns a promise, but the promise does not return a result, Excel will continue showing #BUSY!. Check your functions to make sure that any promises are properly returning a result to a cell.

### Error: The dev server is already running on port 3000

Sometimes when running `npm start` you may see an error that the dev server is already running on port 3000 (or whichever port your add-in uses). You can stop the dev server by running `npm stop` or by closing the Node.js window. But in some cases in can take a few minutes for the dev server to actually stop running.

## Reporting feedback

If you are encountering issues that aren't documented here, let us know. There are two ways to report issues.

### In Excel on Windows or Mac

If using Excel on Windows or Mac, you can report feedback to the Office extensibility team directly from Excel. To do this, select **File -> Feedback -> Send a Frown**. Sending a frown will provide the necessary logs to understand the issue you are hitting.

### In Github

Feel free to submit an issue you encounter either through the "Content feedback" feature at the bottom of any documentation page, or by [filing a new issue directly to the custom functions repository](https://github.com/OfficeDev/Excel-Custom-Functions/issues).

## Next steps
Learn how to [debug your custom functions](custom-functions-debugging.md).

## See also

* [Custom functions metadata autogeneration](custom-functions-json-autogeneration.md)
* [Runtime for Excel custom functions](custom-functions-runtime.md)
* [Custom functions best practices](custom-functions-best-practices.md)
* [Make your custom functions compatible with XLL user-defined functions](make-custom-functions-compatible-with-xll-udf.md)
* [Create custom functions in Excel](custom-functions-overview.md)
