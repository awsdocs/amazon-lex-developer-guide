# DeleteBot<a name="API_DeleteBot"></a>

Deletes all versions of the bot, including the `$LATEST` version\. To delete a specific version of the bot, use the [DeleteBotVersion](API_DeleteBotVersion.md) operation\. The `DeleteBot` operation doesn't immediately remove the bot schema\. Instead, it is marked for deletion and removed later\.

Amazon Lex stores utterances indefinitely for improving the ability of your bot to respond to user inputs\. These utterances are not removed when the bot is deleted\. To remove the utterances, use the [DeleteUtterances](API_DeleteUtterances.md) operation\.

If a bot has an alias, you can't delete it\. Instead, the `DeleteBot` operation returns a `ResourceInUseException` exception that includes a reference to the alias that refers to the bot\. To remove the reference to the bot, delete the alias\. If you get the same exception again, delete the referring alias until the `DeleteBot` operation is successful\.

This operation requires permissions for the `lex:DeleteBot` action\.

## Request Syntax<a name="API_DeleteBot_RequestSyntax"></a>

```
DELETE /bots/name HTTP/1.1
```

## URI Request Parameters<a name="API_DeleteBot_RequestParameters"></a>

The request uses the following URI parameters\.

 ** [name](#API_DeleteBot_RequestSyntax) **   <a name="lex-DeleteBot-request-name"></a>
The name of the bot\. The name is case sensitive\.   
Length Constraints: Minimum length of 2\. Maximum length of 50\.  
Pattern: `^([A-Za-z]_?)+$`   
Required: Yes

## Request Body<a name="API_DeleteBot_RequestBody"></a>

The request does not have a request body\.

## Response Syntax<a name="API_DeleteBot_ResponseSyntax"></a>

```
HTTP/1.1 204
```

## Response Elements<a name="API_DeleteBot_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 204 response with an empty HTTP body\.

## Errors<a name="API_DeleteBot_Errors"></a>

 **BadRequestException**   
The request is not well formed\. For example, a value is invalid or a required field is missing\. Check the field values, and try again\.  
HTTP Status Code: 400

 **ConflictException**   
 There was a conflict processing the request\. Try your request again\.   
HTTP Status Code: 409

 **InternalFailureException**   
An internal Amazon Lex error occurred\. Try your request again\.  
HTTP Status Code: 500

 **LimitExceededException**   
The request exceeded a limit\. Try your request again\.  
HTTP Status Code: 429

 **NotFoundException**   
The resource specified in the request was not found\. Check the resource and try again\.  
HTTP Status Code: 404

 **ResourceInUseException**   
The resource that you are attempting to delete is referred to by another resource\. Use this information to remove references to the resource that you are trying to delete\.  
The body of the exception contains a JSON object that describes the resource\.  
 `{ "resourceType": BOT | BOTALIAS | BOTCHANNEL | INTENT,`   
 `"resourceReference": {`   
 `"name": string, "version": string } }`   
HTTP Status Code: 400

## See Also<a name="API_DeleteBot_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/lex-models-2017-04-19/DeleteBot) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/lex-models-2017-04-19/DeleteBot) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/lex-models-2017-04-19/DeleteBot) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/lex-models-2017-04-19/DeleteBot) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/lex-models-2017-04-19/DeleteBot) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/lex-models-2017-04-19/DeleteBot) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/lex-models-2017-04-19/DeleteBot) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/lex-models-2017-04-19/DeleteBot) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/lex-models-2017-04-19/DeleteBot) 