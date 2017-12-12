# GetBotChannelAssociation<a name="API_GetBotChannelAssociation"></a>

Returns information about the association between an Amazon Lex bot and a messaging platform\.

This operation requires permissions for the `lex:GetBotChannelAssociation` action\.

## Request Syntax<a name="API_GetBotChannelAssociation_RequestSyntax"></a>

```
GET /bots/botName/aliases/aliasName/channels/name HTTP/1.1
```

## URI Request Parameters<a name="API_GetBotChannelAssociation_RequestParameters"></a>

The request requires the following URI parameters\.

 ** botAlias **   
An alias pointing to the specific version of the Amazon Lex bot to which this association is being made\.  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `^([A-Za-z]_?)+$` 

 ** botName **   
The name of the Amazon Lex bot\.  
Length Constraints: Minimum length of 2\. Maximum length of 50\.  
Pattern: `^([A-Za-z]_?)+$` 

 ** name **   
The name of the association between the bot and the channel\. The name is case sensitive\.   
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `^([A-Za-z]_?)+$` 

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

 ** botAlias **   
An alias pointing to the specific version of the Amazon Lex bot to which this association is being made\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `^([A-Za-z]_?)+$` 

 ** botConfiguration **   
Provides information that the messaging platform needs to communicate with the Amazon Lex bot\.  
Type: String to string map

 ** botName **   
The name of the Amazon Lex bot\.  
Type: String  
Length Constraints: Minimum length of 2\. Maximum length of 50\.  
Pattern: `^([A-Za-z]_?)+$` 

 ** createdDate **   
The date that the association between the bot and the channel was created\.  
Type: Timestamp

 ** description **   
A description of the association between the bot and the channel\.  
Type: String  
Length Constraints: Minimum length of 0\. Maximum length of 200\.

 ** failureReason **   
If `status` is `FAILED`, Amazon Lex provides the reason that it failed to create the association\.  
Type: String

 ** name **   
The name of the association between the bot and the channel\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `^([A-Za-z]_?)+$` 

 ** status **   
The status of the bot channel\.   

+  `CREATED` \- The channel has been created and is ready for use\.

+  `IN_PROGRESS` \- Channel creation is in progress\.

+  `FAILED` \- There was an error creating the channel\. For information about the reason for the failure, see the `failureReason` field\.
Type: String  
Valid Values:` IN_PROGRESS | CREATED | FAILED` 

 ** type **   
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

+  [AWS Command Line Interface](http://docs.aws.amazon.com/goto/aws-cli/lex-models-2017-04-19/GetBotChannelAssociation) 

+  [AWS SDK for \.NET](http://docs.aws.amazon.com/goto/DotNetSDKV3/lex-models-2017-04-19/GetBotChannelAssociation) 

+  [AWS SDK for C\+\+](http://docs.aws.amazon.com/goto/SdkForCpp/lex-models-2017-04-19/GetBotChannelAssociation) 

+  [AWS SDK for Go](http://docs.aws.amazon.com/goto/SdkForGoV1/lex-models-2017-04-19/GetBotChannelAssociation) 

+  [AWS SDK for Java](http://docs.aws.amazon.com/goto/SdkForJava/lex-models-2017-04-19/GetBotChannelAssociation) 

+  [AWS SDK for JavaScript](http://docs.aws.amazon.com/goto/AWSJavaScriptSDK/lex-models-2017-04-19/GetBotChannelAssociation) 

+  [AWS SDK for PHP V3](http://docs.aws.amazon.com/goto/SdkForPHPV3/lex-models-2017-04-19/GetBotChannelAssociation) 

+  [AWS SDK for Python](http://docs.aws.amazon.com/goto/boto3/lex-models-2017-04-19/GetBotChannelAssociation) 

+  [AWS SDK for Ruby V2](http://docs.aws.amazon.com/goto/SdkForRubyV2/lex-models-2017-04-19/GetBotChannelAssociation) 