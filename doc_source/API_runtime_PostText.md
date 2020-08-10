# PostText<a name="API_runtime_PostText"></a>

Sends user input to Amazon Lex\. Client applications can use this API to send requests to Amazon Lex at runtime\. Amazon Lex then interprets the user input using the machine learning model it built for the bot\. 

 In response, Amazon Lex returns the next `message` to convey to the user an optional `responseCard` to display\. Consider the following example messages: 
+  For a user input "I would like a pizza", Amazon Lex might return a response with a message eliciting slot data \(for example, PizzaSize\): "What size pizza would you like?" 
+  After the user provides all of the pizza order information, Amazon Lex might return a response with a message to obtain user confirmation "Proceed with the pizza order?"\. 
+  After the user replies to a confirmation prompt with a "yes", Amazon Lex might return a conclusion statement: "Thank you, your cheese pizza has been ordered\."\. 

 Not all Amazon Lex messages require a user response\. For example, a conclusion statement does not require a response\. Some messages require only a "yes" or "no" user response\. In addition to the `message`, Amazon Lex provides additional context about the message in the response that you might use to enhance client behavior, for example, to display the appropriate client user interface\. These are the `slotToElicit`, `dialogState`, `intentName`, and `slots` fields in the response\. Consider the following examples: 
+ If the message is to elicit slot data, Amazon Lex returns the following context information:
  +  `dialogState` set to ElicitSlot 
  +  `intentName` set to the intent name in the current context 
  +  `slotToElicit` set to the slot name for which the `message` is eliciting information 
  +  `slots` set to a map of slots, configured for the intent, with currently known values 
+  If the message is a confirmation prompt, the `dialogState` is set to ConfirmIntent and `SlotToElicit` is set to null\. 
+ If the message is a clarification prompt \(configured for the intent\) that indicates that user intent is not understood, the `dialogState` is set to ElicitIntent and `slotToElicit` is set to null\. 

 In addition, Amazon Lex also returns your application\-specific `sessionAttributes`\. For more information, see [Managing Conversation Context](https://docs.aws.amazon.com/lex/latest/dg/context-mgmt.html)\. 

## Request Syntax<a name="API_runtime_PostText_RequestSyntax"></a>

```
POST /bot/botName/alias/botAlias/user/userId/text HTTP/1.1
Content-type: application/json

{
   "inputText": "string",
   "requestAttributes": { 
      "string" : "string" 
   },
   "sessionAttributes": { 
      "string" : "string" 
   }
}
```

## URI Request Parameters<a name="API_runtime_PostText_RequestParameters"></a>

The request uses the following URI parameters\.

 ** [botAlias](#API_runtime_PostText_RequestSyntax) **   <a name="lex-runtime_PostText-request-botAlias"></a>
The alias of the Amazon Lex bot\.  
Required: Yes

 ** [botName](#API_runtime_PostText_RequestSyntax) **   <a name="lex-runtime_PostText-request-botName"></a>
The name of the Amazon Lex bot\.  
Required: Yes

 ** [userId](#API_runtime_PostText_RequestSyntax) **   <a name="lex-runtime_PostText-request-userId"></a>
The ID of the client application user\. Amazon Lex uses this to identify a user's conversation with your bot\. At runtime, each request must contain the `userID` field\.  
To decide the user ID to use for your application, consider the following factors\.  
+ The `userID` field must not contain any personally identifiable information of the user, for example, name, personal identification numbers, or other end user personal information\.
+ If you want a user to start a conversation on one device and continue on another device, use a user\-specific identifier\.
+ If you want the same user to be able to have two independent conversations on two different devices, choose a device\-specific identifier\.
+ A user can't have two independent conversations with two different versions of the same bot\. For example, a user can't have a conversation with the PROD and BETA versions of the same bot\. If you anticipate that a user will need to have conversation with two different versions, for example, while testing, include the bot alias in the user ID to separate the two conversations\.
Length Constraints: Minimum length of 2\. Maximum length of 100\.  
Pattern: `[0-9a-zA-Z._:-]+`   
Required: Yes

## Request Body<a name="API_runtime_PostText_RequestBody"></a>

The request accepts the following data in JSON format\.

 ** [inputText](#API_runtime_PostText_RequestSyntax) **   <a name="lex-runtime_PostText-request-inputText"></a>
The text that the user entered \(Amazon Lex interprets this text\)\.  
When you are using the AWS CLI, you can't pass a URL in the `--input-text` parameter\. Pass the URL using the `--cli-input-json` parameter instead\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 1024\.  
Required: Yes

 ** [requestAttributes](#API_runtime_PostText_RequestSyntax) **   <a name="lex-runtime_PostText-request-requestAttributes"></a>
Request\-specific information passed between Amazon Lex and a client application\.  
The namespace `x-amz-lex:` is reserved for special attributes\. Don't create any request attributes with the prefix `x-amz-lex:`\.  
For more information, see [Setting Request Attributes](https://docs.aws.amazon.com/lex/latest/dg/context-mgmt.html#context-mgmt-request-attribs)\.  
Type: String to string map  
Required: No

 ** [sessionAttributes](#API_runtime_PostText_RequestSyntax) **   <a name="lex-runtime_PostText-request-sessionAttributes"></a>
Application\-specific information passed between Amazon Lex and a client application\.  
For more information, see [Setting Session Attributes](https://docs.aws.amazon.com/lex/latest/dg/context-mgmt.html#context-mgmt-session-attribs)\.  
Type: String to string map  
Required: No

## Response Syntax<a name="API_runtime_PostText_ResponseSyntax"></a>

```
HTTP/1.1 200
Content-type: application/json

{
   "alternativeIntents": [ 
      { 
         "intentName": "string",
         "nluIntentConfidence": { 
            "score": number
         },
         "slots": { 
            "string" : "string" 
         }
      }
   ],
   "botVersion": "string",
   "dialogState": "string",
   "intentName": "string",
   "message": "string",
   "messageFormat": "string",
   "nluIntentConfidence": { 
      "score": number
   },
   "responseCard": { 
      "contentType": "string",
      "genericAttachments": [ 
         { 
            "attachmentLinkUrl": "string",
            "buttons": [ 
               { 
                  "text": "string",
                  "value": "string"
               }
            ],
            "imageUrl": "string",
            "subTitle": "string",
            "title": "string"
         }
      ],
      "version": "string"
   },
   "sentimentResponse": { 
      "sentimentLabel": "string",
      "sentimentScore": "string"
   },
   "sessionAttributes": { 
      "string" : "string" 
   },
   "sessionId": "string",
   "slots": { 
      "string" : "string" 
   },
   "slotToElicit": "string"
}
```

## Response Elements<a name="API_runtime_PostText_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [alternativeIntents](#API_runtime_PostText_ResponseSyntax) **   <a name="lex-runtime_PostText-response-alternativeIntents"></a>
One to four alternative intents that may be applicable to the user's intent\.  
Each alternative includes a score that indicates how confident Amazon Lex is that the intent matches the user's intent\. The intents are sorted by the confidence score\.  
Type: Array of [PredictedIntent](API_runtime_PredictedIntent.md) objects  
Array Members: Maximum number of 4 items\.

 ** [botVersion](#API_runtime_PostText_ResponseSyntax) **   <a name="lex-runtime_PostText-response-botVersion"></a>
The version of the bot that responded to the conversation\. You can use this information to help determine if one version of a bot is performing better than another version\.  
If you have enabled the new natural language understanding \(NLU\) model, you can use this to determine if the improvement is due to changes to the bot or changes to the NLU\.  
For more information about enabling the new NLU, see the [enableModelImprovements](https://docs.aws.amazon.com/lex/latest/dg/API_PutBot.html#lex-PutBot-request-enableModelImprovements) parameter of the `PutBot` operation\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 64\.  
Pattern: `[0-9]+|\$LATEST` 

 ** [dialogState](#API_runtime_PostText_ResponseSyntax) **   <a name="lex-runtime_PostText-response-dialogState"></a>
 Identifies the current state of the user interaction\. Amazon Lex returns one of the following values as `dialogState`\. The client can optionally use this information to customize the user interface\.   
+  `ElicitIntent` \- Amazon Lex wants to elicit user intent\. 

  For example, a user might utter an intent \("I want to order a pizza"\)\. If Amazon Lex cannot infer the user intent from this utterance, it will return this dialogState\.
+  `ConfirmIntent` \- Amazon Lex is expecting a "yes" or "no" response\. 

   For example, Amazon Lex wants user confirmation before fulfilling an intent\. 

  Instead of a simple "yes" or "no," a user might respond with additional information\. For example, "yes, but make it thick crust pizza" or "no, I want to order a drink"\. Amazon Lex can process such additional information \(in these examples, update the crust type slot value, or change intent from OrderPizza to OrderDrink\)\.
+  `ElicitSlot` \- Amazon Lex is expecting a slot value for the current intent\. 

  For example, suppose that in the response Amazon Lex sends this message: "What size pizza would you like?"\. A user might reply with the slot value \(e\.g\., "medium"\)\. The user might also provide additional information in the response \(e\.g\., "medium thick crust pizza"\)\. Amazon Lex can process such additional information appropriately\. 
+  `Fulfilled` \- Conveys that the Lambda function configured for the intent has successfully fulfilled the intent\. 
+  `ReadyForFulfillment` \- Conveys that the client has to fulfill the intent\. 
+  `Failed` \- Conveys that the conversation with the user failed\. 

   This can happen for various reasons including that the user did not provide an appropriate response to prompts from the service \(you can configure how many times Amazon Lex can prompt a user for specific information\), or the Lambda function failed to fulfill the intent\. 
Type: String  
Valid Values:` ElicitIntent | ConfirmIntent | ElicitSlot | Fulfilled | ReadyForFulfillment | Failed` 

 ** [intentName](#API_runtime_PostText_ResponseSyntax) **   <a name="lex-runtime_PostText-response-intentName"></a>
The current user intent that Amazon Lex is aware of\.  
Type: String

 ** [message](#API_runtime_PostText_ResponseSyntax) **   <a name="lex-runtime_PostText-response-message"></a>
The message to convey to the user\. The message can come from the bot's configuration or from a Lambda function\.  
If the intent is not configured with a Lambda function, or if the Lambda function returned `Delegate` as the `dialogAction.type` its response, Amazon Lex decides on the next course of action and selects an appropriate message from the bot's configuration based on the current interaction context\. For example, if Amazon Lex isn't able to understand user input, it uses a clarification prompt message\.  
When you create an intent you can assign messages to groups\. When messages are assigned to groups Amazon Lex returns one message from each group in the response\. The message field is an escaped JSON string containing the messages\. For more information about the structure of the JSON string returned, see [Supported Message Formats](howitworks-manage-prompts.md#msg-prompts-formats)\.  
If the Lambda function returns a message, Amazon Lex passes it to the client in its response\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 1024\.

 ** [messageFormat](#API_runtime_PostText_ResponseSyntax) **   <a name="lex-runtime_PostText-response-messageFormat"></a>
The format of the response message\. One of the following values:  
+  `PlainText` \- The message contains plain UTF\-8 text\.
+  `CustomPayload` \- The message is a custom format defined by the Lambda function\.
+  `SSML` \- The message contains text formatted for voice output\.
+  `Composite` \- The message contains an escaped JSON object containing one or more messages from the groups that messages were assigned to when the intent was created\.
Type: String  
Valid Values:` PlainText | CustomPayload | SSML | Composite` 

 ** [nluIntentConfidence](#API_runtime_PostText_ResponseSyntax) **   <a name="lex-runtime_PostText-response-nluIntentConfidence"></a>
Provides a score that indicates how confident Amazon Lex is that the returned intent is the one that matches the user's intent\. The score is between 0\.0 and 1\.0\. For more information, see [Confidence Scores](https://docs.aws.amazon.com/lex/latest/dg/confidence-scores.html)\.  
The score is a relative score, not an absolute score\. The score may change based on improvements to the Amazon Lex natural language understanding \(NLU\) model\.  
Type: [IntentConfidence](API_runtime_IntentConfidence.md) object

 ** [responseCard](#API_runtime_PostText_ResponseSyntax) **   <a name="lex-runtime_PostText-response-responseCard"></a>
Represents the options that the user has to respond to the current prompt\. Response Card can come from the bot configuration \(in the Amazon Lex console, choose the settings button next to a slot\) or from a code hook \(Lambda function\)\.   
Type: [ResponseCard](API_runtime_ResponseCard.md) object

 ** [sentimentResponse](#API_runtime_PostText_ResponseSyntax) **   <a name="lex-runtime_PostText-response-sentimentResponse"></a>
The sentiment expressed in and utterance\.  
When the bot is configured to send utterances to Amazon Comprehend for sentiment analysis, this field contains the result of the analysis\.  
Type: [SentimentResponse](API_runtime_SentimentResponse.md) object

 ** [sessionAttributes](#API_runtime_PostText_ResponseSyntax) **   <a name="lex-runtime_PostText-response-sessionAttributes"></a>
A map of key\-value pairs representing the session\-specific context information\.  
Type: String to string map

 ** [sessionId](#API_runtime_PostText_ResponseSyntax) **   <a name="lex-runtime_PostText-response-sessionId"></a>
A unique identifier for the session\.  
Type: String

 ** [slots](#API_runtime_PostText_ResponseSyntax) **   <a name="lex-runtime_PostText-response-slots"></a>
 The intent slots that Amazon Lex detected from the user input in the conversation\.   
Amazon Lex creates a resolution list containing likely values for a slot\. The value that it returns is determined by the `valueSelectionStrategy` selected when the slot type was created or updated\. If `valueSelectionStrategy` is set to `ORIGINAL_VALUE`, the value provided by the user is returned, if the user value is similar to the slot values\. If `valueSelectionStrategy` is set to `TOP_RESOLUTION` Amazon Lex returns the first value in the resolution list or, if there is no resolution list, null\. If you don't specify a `valueSelectionStrategy`, the default is `ORIGINAL_VALUE`\.  
Type: String to string map

 ** [slotToElicit](#API_runtime_PostText_ResponseSyntax) **   <a name="lex-runtime_PostText-response-slotToElicit"></a>
If the `dialogState` value is `ElicitSlot`, returns the name of the slot for which Amazon Lex is eliciting a value\.   
Type: String

## Errors<a name="API_runtime_PostText_Errors"></a>

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

 **LoopDetectedException**   
This exception is not used\.  
HTTP Status Code: 508

 **NotFoundException**   
The resource \(such as the Amazon Lex bot or an alias\) that is referred to is not found\.  
HTTP Status Code: 404

## See Also<a name="API_runtime_PostText_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/runtime.lex-2016-11-28/PostText) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/runtime.lex-2016-11-28/PostText) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/runtime.lex-2016-11-28/PostText) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/runtime.lex-2016-11-28/PostText) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/runtime.lex-2016-11-28/PostText) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/runtime.lex-2016-11-28/PostText) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/runtime.lex-2016-11-28/PostText) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/runtime.lex-2016-11-28/PostText) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/runtime.lex-2016-11-28/PostText) 