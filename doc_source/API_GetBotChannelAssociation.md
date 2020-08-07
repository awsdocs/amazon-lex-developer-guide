# GetBotChannelAssociation<a name="API_GetBotChannelAssociation"></a>

Returns information about the association between an Amazon Lex bot and a messaging platform\.

This operation requires permissions for the `lex:GetBotChannelAssociation` action\.

## Request Syntax<a name="API_GetBotChannelAssociation_RequestSyntax"></a>

```
GET /bots/botName/aliases/aliasName/channels/name HTTP/1.1
```

## URI Request Parameters<a name="API_GetBotChannelAssociation_RequestParameters"></a>

The request uses the following URI parameters\.

 ** [aliasName](#API_GetBotChannelAssociation_RequestSyntax) **   <a name="lex-GetBotChannelAssociation-request-botAlias"></a>
An alias pointing to the specific version of the Amazon Lex bot to which this association is being made\.  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `^([A-Za-z]_?)+$`   
Required: Yes

 ** [botName](#API_GetBotChannelAssociation_RequestSyntax) **   <a name="lex-GetBotChannelAssociation-request-botName"></a>
The name of the Amazon Lex bot\.  
Length Constraints: Minimum length of 2\. Maximum length of 50\.  
Pattern: `^([A-Za-z]_?)+$`   
Required: Yes

 ** [name](#API_GetBotChannelAssociation_RequestSyntax) **   <a name="lex-GetBotChannelAssociation-request-name"></a>
The name of the association between the bot and the channel\. The name is case sensitive\.   
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `^([A-Za-z]_?)+$`   
Required: Yes

## Request Body<a name="API_GetBotChannelAssociation_RequestBody"></a>

The request does not have a request body\.

## Response Syntax<a name="API_GetBotChannelAssociation_ResponseSyntax"></a>

```
HTTP/1.1 200
Content-type: application/json

{
   "botAlias": "string",
   "botConfiguration": { 
      "string" : "string" 
   },
   "botName": "string",
   "createdDate": number,
   "description": "string",
   "failureReason": "string",
   "name": "string",
   "status": "string",
   "type": "string"
}
```

## Response Elements<a name="API_GetBotChannelAssociation_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [botAlias](#API_GetBotChannelAssociation_ResponseSyntax) **   <a name="lex-GetBotChannelAssociation-response-botAlias"></a>
An alias pointing to the specific version of the Amazon Lex bot to which this association is being made\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `^([A-Za-z]_?)+$` 

 ** [botConfiguration](#API_GetBotChannelAssociation_ResponseSyntax) **   <a name="lex-GetBotChannelAssociation-response-botConfiguration"></a>
Provides information that the messaging platform needs to communicate with the Amazon Lex bot\.  
Type: String to string map  
Map Entries: Maximum number of 10 items\.

 ** [botName](#API_GetBotChannelAssociation_ResponseSyntax) **   <a name="lex-GetBotChannelAssociation-response-botName"></a>
The name of the Amazon Lex bot\.  
Type: String  
Length Constraints: Minimum length of 2\. Maximum length of 50\.  
Pattern: `^([A-Za-z]_?)+$` 

 ** [createdDate](#API_GetBotChannelAssociation_ResponseSyntax) **   <a name="lex-GetBotChannelAssociation-response-createdDate"></a>
The date that the association between the bot and the channel was created\.  
Type: Timestamp

 ** [description](#API_GetBotChannelAssociation_ResponseSyntax) **   <a name="lex-GetBotChannelAssociation-response-description"></a>
A description of the association between the bot and the channel\.  
Type: String  
Length Constraints: Minimum length of 0\. Maximum length of 200\.

 ** [failureReason](#API_GetBotChannelAssociation_ResponseSyntax) **   <a name="lex-GetBotChannelAssociation-response-failureReason"></a>
If `status` is `FAILED`, Amazon Lex provides the reason that it failed to create the association\.  
Type: String

 ** [name](#API_GetBotChannelAssociation_ResponseSyntax) **   <a name="lex-GetBotChannelAssociation-response-name"></a>
The name of the association between the bot and the channel\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `^([A-Za-z]_?)+$` 

 ** [status](#API_GetBotChannelAssociation_ResponseSyntax) **   <a name="lex-GetBotChannelAssociation-response-status"></a>
The status of the bot channel\.   
+  `CREATED` \- The channel has been created and is ready for use\.
+  `IN_PROGRESS` \- Channel creation is in progress\.
+  `FAILED` \- There was an error creating the channel\. For information about the reason for the failure, see the `failureReason` field\.
Type: String  
Valid Values:` IN_PROGRESS | CREATED | FAILED` 

 ** [type](#API_GetBotChannelAssociation_ResponseSyntax) **   <a name="lex-GetBotChannelAssociation-response-type"></a>
The type of the messaging platform\.  
Type: String  
Valid Values:` Facebook | Slack | Twilio-Sms | Kik` 

## Errors<a name="API_GetBotChannelAssociation_Errors"></a>

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

## See Also<a name="API_GetBotChannelAssociation_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/lex-models-2017-04-19/GetBotChannelAssociation) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/lex-models-2017-04-19/GetBotChannelAssociation) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/lex-models-2017-04-19/GetBotChannelAssociation) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/lex-models-2017-04-19/GetBotChannelAssociation) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/lex-models-2017-04-19/GetBotChannelAssociation) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/lex-models-2017-04-19/GetBotChannelAssociation) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/lex-models-2017-04-19/GetBotChannelAssociation) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/lex-models-2017-04-19/GetBotChannelAssociation) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/lex-models-2017-04-19/GetBotChannelAssociation) 