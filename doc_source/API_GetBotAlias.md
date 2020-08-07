# GetBotAlias<a name="API_GetBotAlias"></a>

Returns information about an Amazon Lex bot alias\. For more information about aliases, see [Versioning and Aliases](versioning-aliases.md)\.

This operation requires permissions for the `lex:GetBotAlias` action\.

## Request Syntax<a name="API_GetBotAlias_RequestSyntax"></a>

```
GET /bots/botName/aliases/name HTTP/1.1
```

## URI Request Parameters<a name="API_GetBotAlias_RequestParameters"></a>

The request uses the following URI parameters\.

 ** [botName](#API_GetBotAlias_RequestSyntax) **   <a name="lex-GetBotAlias-request-botName"></a>
The name of the bot\.  
Length Constraints: Minimum length of 2\. Maximum length of 50\.  
Pattern: `^([A-Za-z]_?)+$`   
Required: Yes

 ** [name](#API_GetBotAlias_RequestSyntax) **   <a name="lex-GetBotAlias-request-name"></a>
The name of the bot alias\. The name is case sensitive\.  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `^([A-Za-z]_?)+$`   
Required: Yes

## Request Body<a name="API_GetBotAlias_RequestBody"></a>

The request does not have a request body\.

## Response Syntax<a name="API_GetBotAlias_ResponseSyntax"></a>

```
HTTP/1.1 200
Content-type: application/json

{
   "botName": "string",
   "botVersion": "string",
   "checksum": "string",
   "conversationLogs": { 
      "iamRoleArn": "string",
      "logSettings": [ 
         { 
            "destination": "string",
            "kmsKeyArn": "string",
            "logType": "string",
            "resourceArn": "string",
            "resourcePrefix": "string"
         }
      ]
   },
   "createdDate": number,
   "description": "string",
   "lastUpdatedDate": number,
   "name": "string"
}
```

## Response Elements<a name="API_GetBotAlias_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [botName](#API_GetBotAlias_ResponseSyntax) **   <a name="lex-GetBotAlias-response-botName"></a>
The name of the bot that the alias points to\.  
Type: String  
Length Constraints: Minimum length of 2\. Maximum length of 50\.  
Pattern: `^([A-Za-z]_?)+$` 

 ** [botVersion](#API_GetBotAlias_ResponseSyntax) **   <a name="lex-GetBotAlias-response-botVersion"></a>
The version of the bot that the alias points to\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 64\.  
Pattern: `\$LATEST|[0-9]+` 

 ** [checksum](#API_GetBotAlias_ResponseSyntax) **   <a name="lex-GetBotAlias-response-checksum"></a>
Checksum of the bot alias\.  
Type: String

 ** [conversationLogs](#API_GetBotAlias_ResponseSyntax) **   <a name="lex-GetBotAlias-response-conversationLogs"></a>
The settings that determine how Amazon Lex uses conversation logs for the alias\.  
Type: [ConversationLogsResponse](API_ConversationLogsResponse.md) object

 ** [createdDate](#API_GetBotAlias_ResponseSyntax) **   <a name="lex-GetBotAlias-response-createdDate"></a>
The date that the bot alias was created\.  
Type: Timestamp

 ** [description](#API_GetBotAlias_ResponseSyntax) **   <a name="lex-GetBotAlias-response-description"></a>
A description of the bot alias\.  
Type: String  
Length Constraints: Minimum length of 0\. Maximum length of 200\.

 ** [lastUpdatedDate](#API_GetBotAlias_ResponseSyntax) **   <a name="lex-GetBotAlias-response-lastUpdatedDate"></a>
The date that the bot alias was updated\. When you create a resource, the creation date and the last updated date are the same\.  
Type: Timestamp

 ** [name](#API_GetBotAlias_ResponseSyntax) **   <a name="lex-GetBotAlias-response-name"></a>
The name of the bot alias\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `^([A-Za-z]_?)+$` 

## Errors<a name="API_GetBotAlias_Errors"></a>

 **BadRequestException**   
The request is not well formed\. For example, a value is invalid or a required field is missing\. Check the field values, and try again\.  
HTTP Status Code: 400

 **InternalFailureException**   
An internal Amazon Lex error occurred\. Try your request again\.  
HTTP Status Code: 500

 **LimitExceededException**   
The request exceeded a limit\. Try your request again\.  
HTTP Status Code: 429

 **NotFoundException**   
The resource specified in the request was not found\. Check the resource and try again\.  
HTTP Status Code: 404

## See Also<a name="API_GetBotAlias_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/lex-models-2017-04-19/GetBotAlias) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/lex-models-2017-04-19/GetBotAlias) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/lex-models-2017-04-19/GetBotAlias) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/lex-models-2017-04-19/GetBotAlias) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/lex-models-2017-04-19/GetBotAlias) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/lex-models-2017-04-19/GetBotAlias) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/lex-models-2017-04-19/GetBotAlias) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/lex-models-2017-04-19/GetBotAlias) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/lex-models-2017-04-19/GetBotAlias) 