# DeleteBotAlias<a name="API_DeleteBotAlias"></a>

Deletes an alias for the specified bot\. 

You can't delete an alias that is used in the association between a bot and a messaging channel\. If an alias is used in a channel association, the `DeleteBot` operation returns a `ResourceInUseException` exception that includes a reference to the channel association that refers to the bot\. You can remove the reference to the alias by deleting the channel association\. If you get the same exception again, delete the referring association until the `DeleteBotAlias` operation is successful\.

## Request Syntax<a name="API_DeleteBotAlias_RequestSyntax"></a>

```
DELETE /bots/botName/aliases/name HTTP/1.1
```

## URI Request Parameters<a name="API_DeleteBotAlias_RequestParameters"></a>

The request uses the following URI parameters\.

 ** [botName](#API_DeleteBotAlias_RequestSyntax) **   <a name="lex-DeleteBotAlias-request-botName"></a>
The name of the bot that the alias points to\.  
Length Constraints: Minimum length of 2\. Maximum length of 50\.  
Pattern: `^([A-Za-z]_?)+$`   
Required: Yes

 ** [name](#API_DeleteBotAlias_RequestSyntax) **   <a name="lex-DeleteBotAlias-request-name"></a>
The name of the alias to delete\. The name is case sensitive\.   
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `^([A-Za-z]_?)+$`   
Required: Yes

## Request Body<a name="API_DeleteBotAlias_RequestBody"></a>

The request does not have a request body\.

## Response Syntax<a name="API_DeleteBotAlias_ResponseSyntax"></a>

```
HTTP/1.1 204
```

## Response Elements<a name="API_DeleteBotAlias_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 204 response with an empty HTTP body\.

## Errors<a name="API_DeleteBotAlias_Errors"></a>

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

## See Also<a name="API_DeleteBotAlias_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/lex-models-2017-04-19/DeleteBotAlias) 
+  [ AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/lex-models-2017-04-19/DeleteBotAlias) 
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/lex-models-2017-04-19/DeleteBotAlias) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/lex-models-2017-04-19/DeleteBotAlias) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/lex-models-2017-04-19/DeleteBotAlias) 
+  [ AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/lex-models-2017-04-19/DeleteBotAlias) 
+  [ AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/lex-models-2017-04-19/DeleteBotAlias) 
+  [ AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/lex-models-2017-04-19/DeleteBotAlias) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/lex-models-2017-04-19/DeleteBotAlias) 