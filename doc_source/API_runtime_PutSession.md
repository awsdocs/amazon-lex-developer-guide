# PutSession<a name="API_runtime_PutSession"></a>

Creates a new session or modifies an existing session with an Amazon Lex bot\. Use this operation to enable your application to set the state of the bot\.

For more information, see [Managing Sessions](https://docs.aws.amazon.com/lex/latest/dg/how-session-api.html)\.

## Request Syntax<a name="API_runtime_PutSession_RequestSyntax"></a>

```
POST /bot/botName/alias/botAlias/user/userId/session HTTP/1.1
Accept: accept
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
   }
}
```

## URI Request Parameters<a name="API_runtime_PutSession_RequestParameters"></a>

The request uses the following URI parameters\.

 ** [accept](#API_runtime_PutSession_RequestSyntax) **   <a name="lex-runtime_PutSession-request-accept"></a>
The message that Amazon Lex returns in the response can be either text or speech based depending on the value of this field\.  
+ If the value is `text/plain; charset=utf-8`, Amazon Lex returns text in the response\.
+ If the value begins with `audio/`, Amazon Lex returns speech in the response\. Amazon Lex uses Amazon Polly to generate the speech in the configuration that you specify\. For example, if you specify `audio/mpeg` as the value, Amazon Lex returns speech in the MPEG format\.
+ If the value is `audio/pcm`, the speech is returned as `audio/pcm` in 16\-bit, little endian format\.
+ The following are the accepted values:
  +  `audio/mpeg` 
  +  `audio/ogg` 
  +  `audio/pcm` 
  +  `audio/*` \(defaults to mpeg\)
  +  `text/plain; charset=utf-8` 

 ** [botAlias](#API_runtime_PutSession_RequestSyntax) **   <a name="lex-runtime_PutSession-request-botAlias"></a>
The alias in use for the bot that contains the session data\.  
Required: Yes

 ** [botName](#API_runtime_PutSession_RequestSyntax) **   <a name="lex-runtime_PutSession-request-botName"></a>
The name of the bot that contains the session data\.  
Required: Yes

 ** [userId](#API_runtime_PutSession_RequestSyntax) **   <a name="lex-runtime_PutSession-request-userId"></a>
The ID of the client application user\. Amazon Lex uses this to identify a user's conversation with your bot\.   
Length Constraints: Minimum length of 2\. Maximum length of 100\.  
Pattern: `[0-9a-zA-Z._:-]+`   
Required: Yes

## Request Body<a name="API_runtime_PutSession_RequestBody"></a>

The request accepts the following data in JSON format\.

 ** [dialogAction](#API_runtime_PutSession_RequestSyntax) **   <a name="lex-runtime_PutSession-request-dialogAction"></a>
Sets the next action that the bot should take to fulfill the conversation\.  
Type: [DialogAction](API_runtime_DialogAction.md) object  
Required: No

 ** [recentIntentSummaryView](#API_runtime_PutSession_RequestSyntax) **   <a name="lex-runtime_PutSession-request-recentIntentSummaryView"></a>
A summary of the recent intents for the bot\. You can use the intent summary view to set a checkpoint label on an intent and modify attributes of intents\. You can also use it to remove or add intent summary objects to the list\.  
An intent that you modify or add to the list must make sense for the bot\. For example, the intent name must be valid for the bot\. You must provide valid values for:  
+  `intentName` 
+ slot names
+  `slotToElict` 
If you send the `recentIntentSummaryView` parameter in a `PutSession` request, the contents of the new summary view replaces the old summary view\. For example, if a `GetSession` request returns three intents in the summary view and you call `PutSession` with one intent in the summary view, the next call to `GetSession` will only return one intent\.  
Type: Array of [IntentSummary](API_runtime_IntentSummary.md) objects  
Array Members: Minimum number of 0 items\. Maximum number of 3 items\.  
Required: No

 ** [sessionAttributes](#API_runtime_PutSession_RequestSyntax) **   <a name="lex-runtime_PutSession-request-sessionAttributes"></a>
Map of key/value pairs representing the session\-specific context information\. It contains application information passed between Amazon Lex and a client application\.  
Type: String to string map  
Required: No

## Response Syntax<a name="API_runtime_PutSession_ResponseSyntax"></a>

```
HTTP/1.1 200
Content-Type: contentType
x-amz-lex-intent-name: intentName
x-amz-lex-slots: slots
x-amz-lex-session-attributes: sessionAttributes
x-amz-lex-message: message
x-amz-lex-message-format: messageFormat
x-amz-lex-dialog-state: dialogState
x-amz-lex-slot-to-elicit: slotToElicit
x-amz-lex-session-id: sessionId

audioStream
```

## Response Elements<a name="API_runtime_PutSession_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The response returns the following HTTP headers\.

 ** [contentType](#API_runtime_PutSession_ResponseSyntax) **   <a name="lex-runtime_PutSession-response-contentType"></a>
Content type as specified in the `Accept` HTTP header in the request\.

 ** [dialogState](#API_runtime_PutSession_ResponseSyntax) **   <a name="lex-runtime_PutSession-response-dialogState"></a>
+  `ConfirmIntent` \- Amazon Lex is expecting a "yes" or "no" response to confirm the intent before fulfilling an intent\.
+  `ElicitIntent` \- Amazon Lex wants to elicit the user's intent\.
+  `ElicitSlot` \- Amazon Lex is expecting the value of a slot for the current intent\.
+  `Failed` \- Conveys that the conversation with the user has failed\. This can happen for various reasons, including the user does not provide an appropriate response to prompts from the service, or if the Lambda function fails to fulfill the intent\.
+  `Fulfilled` \- Conveys that the Lambda function has sucessfully fulfilled the intent\.
+  `ReadyForFulfillment` \- Conveys that the client has to fulfill the intent\.
Valid Values:` ElicitIntent | ConfirmIntent | ElicitSlot | Fulfilled | ReadyForFulfillment | Failed` 

 ** [intentName](#API_runtime_PutSession_ResponseSyntax) **   <a name="lex-runtime_PutSession-response-intentName"></a>
The name of the current intent\.

 ** [message](#API_runtime_PutSession_ResponseSyntax) **   <a name="lex-runtime_PutSession-response-message"></a>
The next message that should be presented to the user\.  
Length Constraints: Minimum length of 1\. Maximum length of 1024\.

 ** [messageFormat](#API_runtime_PutSession_ResponseSyntax) **   <a name="lex-runtime_PutSession-response-messageFormat"></a>
The format of the response message\. One of the following values:  
+  `PlainText` \- The message contains plain UTF\-8 text\.
+  `CustomPayload` \- The message is a custom format for the client\.
+  `SSML` \- The message contains text formatted for voice output\.
+  `Composite` \- The message contains an escaped JSON object containing one or more messages from the groups that messages were assigned to when the intent was created\.
Valid Values:` PlainText | CustomPayload | SSML | Composite` 

 ** [sessionAttributes](#API_runtime_PutSession_ResponseSyntax) **   <a name="lex-runtime_PutSession-response-sessionAttributes"></a>
Map of key/value pairs representing session\-specific context information\.

 ** [sessionId](#API_runtime_PutSession_ResponseSyntax) **   <a name="lex-runtime_PutSession-response-sessionId"></a>
A unique identifier for the session\.

 ** [slots](#API_runtime_PutSession_ResponseSyntax) **   <a name="lex-runtime_PutSession-response-slots"></a>
Map of zero or more intent slots Amazon Lex detected from the user input during the conversation\.  
Amazon Lex creates a resolution list containing likely values for a slot\. The value that it returns is determined by the `valueSelectionStrategy` selected when the slot type was created or updated\. If `valueSelectionStrategy` is set to `ORIGINAL_VALUE`, the value provided by the user is returned, if the user value is similar to the slot values\. If `valueSelectionStrategy` is set to `TOP_RESOLUTION` Amazon Lex returns the first value in the resolution list or, if there is no resolution list, null\. If you don't specify a `valueSelectionStrategy` the default is `ORIGINAL_VALUE`\. 

 ** [slotToElicit](#API_runtime_PutSession_ResponseSyntax) **   <a name="lex-runtime_PutSession-response-slotToElicit"></a>
If the `dialogState` is `ElicitSlot`, returns the name of the slot for which Amazon Lex is eliciting a value\.

The response returns the following as the HTTP body\.

 ** [audioStream](#API_runtime_PutSession_ResponseSyntax) **   <a name="lex-runtime_PutSession-response-audioStream"></a>
The audio version of the message to convey to the user\.

## Errors<a name="API_runtime_PutSession_Errors"></a>

 **BadGatewayException**   
Either the Amazon Lex bot is still building, or one of the dependent services \(Amazon Polly, AWS Lambda\) failed with an internal service error\.  
HTTP Status Code: 502

 **BadRequestException**   
 Request validation failed, there is no usable message in the context, or the bot build failed, is still in progress, or contains unbuilt changes\.   
HTTP Status Code: 400

 **ConflictException**   
 Two clients are using the same AWS account, Amazon Lex bot, and user ID\.   
HTTP Status Code: 409

 **DependencyFailedException**   
 One of the dependencies, such as AWS Lambda or Amazon Polly, threw an exception\. For example,   
+ If Amazon Lex does not have sufficient permissions to call a Lambda function\.
+ If a Lambda function takes longer than 30 seconds to execute\.
+ If a fulfillment Lambda function returns a `Delegate` dialog action without removing any slot values\.
HTTP Status Code: 424

 **InternalFailureException**   
Internal service error\. Retry the call\.  
HTTP Status Code: 500

 **LimitExceededException**   
Exceeded a limit\.  
HTTP Status Code: 429

 **NotAcceptableException**   
The accept header in the request does not have a valid value\.  
HTTP Status Code: 406

 **NotFoundException**   
The resource \(such as the Amazon Lex bot or an alias\) that is referred to is not found\.  
HTTP Status Code: 404

## See Also<a name="API_runtime_PutSession_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/runtime.lex-2016-11-28/PutSession) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/runtime.lex-2016-11-28/PutSession) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/runtime.lex-2016-11-28/PutSession) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/runtime.lex-2016-11-28/PutSession) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/runtime.lex-2016-11-28/PutSession) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/runtime.lex-2016-11-28/PutSession) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/runtime.lex-2016-11-28/PutSession) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/runtime.lex-2016-11-28/PutSession) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/runtime.lex-2016-11-28/PutSession) 