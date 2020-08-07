# DeleteSession<a name="API_runtime_DeleteSession"></a>

Removes session information for a specified bot, alias, and user ID\. 

## Request Syntax<a name="API_runtime_DeleteSession_RequestSyntax"></a>

```
DELETE /bot/botName/alias/botAlias/user/userId/session HTTP/1.1
```

## URI Request Parameters<a name="API_runtime_DeleteSession_RequestParameters"></a>

The request uses the following URI parameters\.

 ** [botAlias](#API_runtime_DeleteSession_RequestSyntax) **   <a name="lex-runtime_DeleteSession-request-botAlias"></a>
The alias in use for the bot that contains the session data\.  
Required: Yes

 ** [botName](#API_runtime_DeleteSession_RequestSyntax) **   <a name="lex-runtime_DeleteSession-request-botName"></a>
The name of the bot that contains the session data\.  
Required: Yes

 ** [userId](#API_runtime_DeleteSession_RequestSyntax) **   <a name="lex-runtime_DeleteSession-request-userId"></a>
The identifier of the user associated with the session data\.  
Length Constraints: Minimum length of 2\. Maximum length of 100\.  
Pattern: `[0-9a-zA-Z._:-]+`   
Required: Yes

## Request Body<a name="API_runtime_DeleteSession_RequestBody"></a>

The request does not have a request body\.

## Response Syntax<a name="API_runtime_DeleteSession_ResponseSyntax"></a>

```
HTTP/1.1 200
Content-type: application/json

{
   "botAlias": "string",
   "botName": "string",
   "sessionId": "string",
   "userId": "string"
}
```

## Response Elements<a name="API_runtime_DeleteSession_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [botAlias](#API_runtime_DeleteSession_ResponseSyntax) **   <a name="lex-runtime_DeleteSession-response-botAlias"></a>
The alias in use for the bot associated with the session data\.  
Type: String

 ** [botName](#API_runtime_DeleteSession_ResponseSyntax) **   <a name="lex-runtime_DeleteSession-response-botName"></a>
The name of the bot associated with the session data\.  
Type: String

 ** [sessionId](#API_runtime_DeleteSession_ResponseSyntax) **   <a name="lex-runtime_DeleteSession-response-sessionId"></a>
The unique identifier for the session\.  
Type: String

 ** [userId](#API_runtime_DeleteSession_ResponseSyntax) **   <a name="lex-runtime_DeleteSession-response-userId"></a>
The ID of the client application user\.  
Type: String  
Length Constraints: Minimum length of 2\. Maximum length of 100\.  
Pattern: `[0-9a-zA-Z._:-]+` 

## Errors<a name="API_runtime_DeleteSession_Errors"></a>

 **BadRequestException**   
 Request validation failed, there is no usable message in the context, or the bot build failed, is still in progress, or contains unbuilt changes\.   
HTTP Status Code: 400

 **ConflictException**   
 Two clients are using the same AWS account, Amazon Lex bot, and user ID\.   
HTTP Status Code: 409

 **InternalFailureException**   
Internal service error\. Retry the call\.  
HTTP Status Code: 500

 **LimitExceededException**   
Exceeded a limit\.  
HTTP Status Code: 429

 **NotFoundException**   
The resource \(such as the Amazon Lex bot or an alias\) that is referred to is not found\.  
HTTP Status Code: 404

## See Also<a name="API_runtime_DeleteSession_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/runtime.lex-2016-11-28/DeleteSession) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/runtime.lex-2016-11-28/DeleteSession) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/runtime.lex-2016-11-28/DeleteSession) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/runtime.lex-2016-11-28/DeleteSession) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/runtime.lex-2016-11-28/DeleteSession) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/runtime.lex-2016-11-28/DeleteSession) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/runtime.lex-2016-11-28/DeleteSession) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/runtime.lex-2016-11-28/DeleteSession) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/runtime.lex-2016-11-28/DeleteSession) 