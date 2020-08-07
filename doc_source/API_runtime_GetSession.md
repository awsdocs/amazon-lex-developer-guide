# GetSession<a name="API_runtime_GetSession"></a>

Returns session information for a specified bot, alias, and user ID\.

## Request Syntax<a name="API_runtime_GetSession_RequestSyntax"></a>

```
GET /bot/botName/alias/botAlias/user/userId/session/?checkpointLabelFilter=checkpointLabelFilter HTTP/1.1
```

## URI Request Parameters<a name="API_runtime_GetSession_RequestParameters"></a>

The request uses the following URI parameters\.

 ** [botAlias](#API_runtime_GetSession_RequestSyntax) **   <a name="lex-runtime_GetSession-request-botAlias"></a>
The alias in use for the bot that contains the session data\.  
Required: Yes

 ** [botName](#API_runtime_GetSession_RequestSyntax) **   <a name="lex-runtime_GetSession-request-botName"></a>
The name of the bot that contains the session data\.  
Required: Yes

 ** [checkpointLabelFilter](#API_runtime_GetSession_RequestSyntax) **   <a name="lex-runtime_GetSession-request-checkpointLabelFilter"></a>
A string used to filter the intents returned in the `recentIntentSummaryView` structure\.   
When you specify a filter, only intents with their `checkpointLabel` field set to that string are returned\.  
Length Constraints: Minimum length of 1\. Maximum length of 255\.  
Pattern: `[a-zA-Z0-9-]+` 

 ** [userId](#API_runtime_GetSession_RequestSyntax) **   <a name="lex-runtime_GetSession-request-userId"></a>
The ID of the client application user\. Amazon Lex uses this to identify a user's conversation with your bot\.   
Length Constraints: Minimum length of 2\. Maximum length of 100\.  
Pattern: `[0-9a-zA-Z._:-]+`   
Required: Yes

## Request Body<a name="API_runtime_GetSession_RequestBody"></a>

The request does not have a request body\.

## Response Syntax<a name="API_runtime_GetSession_ResponseSyntax"></a>

```
HTTP/1.1 200
Content-type: application/json

{
   "dialogAction": { 
      "fulfillmentState": "string",
      "intentName": "string",
      "message": "string",
      "messageFormat": "string",
      "slots": { 
         "string" : "string" 
      },
      "slotToElicit": "string",
      "type": "string"
   },
   "recentIntentSummaryView": [ 
      { 
         "checkpointLabel": "string",
         "confirmationStatus": "string",
         "dialogActionType": "string",
         "fulfillmentState": "string",
         "intentName": "string",
         "slots": { 
            "string" : "string" 
         },
         "slotToElicit": "string"
      }
   ],
   "sessionAttributes": { 
      "string" : "string" 
   },
   "sessionId": "string"
}
```

## Response Elements<a name="API_runtime_GetSession_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [dialogAction](#API_runtime_GetSession_ResponseSyntax) **   <a name="lex-runtime_GetSession-response-dialogAction"></a>
Describes the current state of the bot\.  
Type: [DialogAction](API_runtime_DialogAction.md) object

 ** [recentIntentSummaryView](#API_runtime_GetSession_ResponseSyntax) **   <a name="lex-runtime_GetSession-response-recentIntentSummaryView"></a>
An array of information about the intents used in the session\. The array can contain a maximum of three summaries\. If more than three intents are used in the session, the `recentIntentSummaryView` operation contains information about the last three intents used\.  
If you set the `checkpointLabelFilter` parameter in the request, the array contains only the intents with the specified label\.  
Type: Array of [IntentSummary](API_runtime_IntentSummary.md) objects  
Array Members: Minimum number of 0 items\. Maximum number of 3 items\.

 ** [sessionAttributes](#API_runtime_GetSession_ResponseSyntax) **   <a name="lex-runtime_GetSession-response-sessionAttributes"></a>
Map of key/value pairs representing the session\-specific context information\. It contains application information passed between Amazon Lex and a client application\.  
Type: String to string map

 ** [sessionId](#API_runtime_GetSession_ResponseSyntax) **   <a name="lex-runtime_GetSession-response-sessionId"></a>
A unique identifier for the session\.  
Type: String

## Errors<a name="API_runtime_GetSession_Errors"></a>

 **BadRequestException**   
 Request validation failed, there is no usable message in the context, or the bot build failed, is still in progress, or contains unbuilt changes\.   
HTTP Status Code: 400

 **InternalFailureException**   
Internal service error\. Retry the call\.  
HTTP Status Code: 500

 **LimitExceededException**   
Exceeded a limit\.  
HTTP Status Code: 429

 **NotFoundException**   
The resource \(such as the Amazon Lex bot or an alias\) that is referred to is not found\.  
HTTP Status Code: 404

## See Also<a name="API_runtime_GetSession_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/runtime.lex-2016-11-28/GetSession) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/runtime.lex-2016-11-28/GetSession) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/runtime.lex-2016-11-28/GetSession) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/runtime.lex-2016-11-28/GetSession) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/runtime.lex-2016-11-28/GetSession) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/runtime.lex-2016-11-28/GetSession) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/runtime.lex-2016-11-28/GetSession) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/runtime.lex-2016-11-28/GetSession) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/runtime.lex-2016-11-28/GetSession) 