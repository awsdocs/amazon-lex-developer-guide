# Managing Messages<a name="howitworks-manage-prompts"></a>


+ [Types of Messages](#msg-prompts-msg-types)
+ [Contexts for Configuring Messages](#msg-prompts-context-for-msgs)
+ [Supported Message Formats](#msg-prompts-formats)
+ [Message Groups](#message-groups)
+ [Response Cards](#msg-prompts-resp-card)

When you create a bot, you can configure clarifying or informational messages that you want it to send to the client\. Consider the following examples:

+ You could configure your bot with the following clarification prompt: 

  ```
  I don't understand. What would you like to do?
  ```

  Amazon Lex sends this message to the client if it doesn't understand the user's intent\. 

   

+ Suppose that you create a bot to support an intent called `OrderPizza`\. For a pizza order, you want users to provide information such as pizza size, toppings, and crust type\. You could configure the following prompts:

  ```
  What size pizza do you want?
  What toppings do you want?
  Do you want thick or thin crust?
  ```

  After Amazon Lex determines the user's intent to order pizza, it sends these messages to the client to get information from the user\.

This section explains designing user interactions in your bot configuration\. 

## Types of Messages<a name="msg-prompts-msg-types"></a>

A message can be a prompt or a statement\.

+ A *prompt* is typically a question and expects a user response\. 

+ A *statement* is informational\. It doesn’t expect a response\.

A message can include references to slot and session attributes\. At runtime, Amazon Lex substitutes these references with actual values\. 

To refer to slots values that have been set, use the following syntax:

```
{SlotName} 
```

To refer to session attributes, use the following syntax:

```
[AttributeName] 
```

Messages can include both slot values and session attributes\. 

For example, suppose that you configure the following message in your bot's OrderPizza intent:

```
"Hey [FirstName], your {PizzaTopping} pizza will arrive in [DeliveryTime] minutes." 
```

This message refers to both slot \(`PizzaTopping`\) and session attributes \(`FirstName` and `DeliveryTime`\)\. At runtime, Amazon Lex replaces these placeholders with values and returns the following message to the client:

```
"Hey John, your cheese pizza will arrive in 30 minutes." 
```

To include brackets \(\[\]\) or braces \(\{\}\) in a message, use the backslash \(\\\) escape character\. For example, the following message includes the curly braces and square brackets: 

```
\{Text\} \[Text\]
```

The text returned to the client application looks like this:

```
{Text} [Text]
```

For information about session attributes, see the runtime API operations [PostText](API_runtime_PostText.md) and [PostContent](API_runtime_PostContent.md)\. For an example, see [Example Bot: BookTrip](ex-book-trip.md)\. 

Lambda functions can also generate messages and return them to Amazon Lex to send to the user\. If you add Lambda functions when you configure your intent, you can create messages dynamically\. By providing the messages while configuring your bot, you can eliminate the need to construct a prompt in your Lambda function\.

## Contexts for Configuring Messages<a name="msg-prompts-context-for-msgs"></a>

When you are creating your bot, you can create messages in different contexts, such as clarification prompts in bot, prompts for slot values, and messages from intents\. Amazon Lex chooses an appropriate message in each context to return to your user\. You can provide a group of messages for each context\. If you do, Amazon Lex randomly chooses one message from the group\. You can also specify the format of the message or group the messages together\. For more information, see [Supported Message Formats](#msg-prompts-formats)\.

If you have a Lambda function associated with an intent, you can override any of the messages that you configured at build time\. A Lambda function is not required to use any of these messages, however\.

### Bot Messages<a name="msg-prompts-bot"></a>

You can configure your bot with clarification prompts and hang\-up messages\. At runtime, Amazon Lex uses the clarification prompt** if it doesn't understand the user's intent\. You can configure the number of times that Amazon Lex requests clarification before hanging up with the hang\-up message\. You configure bot\-level messages in the **Error Handling** section of the Amazon Lex console, as follows:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lex/latest/dg/images/how-works-20.png)

With the API, you configure messages by setting the `clarificationPrompt` and `abortStatement` fields in the [PutBot](API_PutBot.md) operation\.

If you use a Lambda function with an intent, the Lambda function might return a response directing Amazon Lex to ask a user's intent\. If the Lambda function doesn’t provide such a message, Amazon Lex uses the clarification prompt\.

### Slot Prompts<a name="msg-prompts-slots"></a>

You must specify at least one prompt message for each of the required slots in an intent\. At runtime, Amazon Lex uses one of these messages to prompt the user to provide a value for the slot\. For example, for a `cityName` slot, the following is a valid prompt: 

```
Which city would you like to fly to?
```

You can set one or more prompts for each slot using the console\. You can also create groups of prompts using the [PutIntent](API_PutIntent.md) operation\. For more information, see [Message Groups](#message-groups)\.

### Responses<a name="msg-prompts-response"></a>

In the console, use the **Responses** section to build dynamic, engaging conversations for your bot\. You can create one or more message groups for a response\. At runtime, Amazon Lex builds a response by selecting one message from each message group\. For more information about message groups, see [Message Groups](#message-groups)\. 

For example, your first message group could contain different greetings: "Hello," "Hi," and "Greetings\." The second message group could contain different forms of introduction: "I am the reservation bot" and "This is the reservation bot\." A third message group could communicate the bot's capabilities: "I can help with car rentals and hotel reservations," "You can make car rentals and hotel reservations," and "I can help you rent a car and book a hotel\."

Lex uses a message from each of the message groups to dynamically build the responses in a conversation\. For example, one interaction could be:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lex/latest/dg/images/default-response-10b.png)

Another one could be:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lex/latest/dg/images/default-response-20c.png)

In either case, the user could respond with a new intent, such as the `BookCar` or `BookHotel` intent\.

You can set up the bot to ask a follow\-up question in the response\. For example, for the preceding interaction, you could create a fourth message group with the following questions: "Can I help with a car or a hotel?", "Would you like to make a reservation now?", and "Is there anything that I can do for you?"\. For messages that include "No" as a response, you can create a follow\-up prompt\. For example:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lex/latest/dg/images/default-response-25a.png)

To create a follow\-up prompt, choose **Wait for user reply**\. Then type the message or messages that you want to send when the user says "No\." When you create a response to use as a follow\-up prompt, you must also specify an appropriate statement when the answer to the statement is "No\." For example:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lex/latest/dg/images/default-response-30b.png)

To add responses to an intent with the API, use the `PutIntent` operation\. To specify a response, set the `conclusionStatement` field in the `PutIntent` request\. To set a follow\-up prompt, set the `followUpPrompt` field and include the statement to send when the user says "No\." You can't set both the `conclusionStatement` field and the `followUpPrompt` field on the same intent\.

## Supported Message Formats<a name="msg-prompts-formats"></a>

When you use the [ PostText Service: Amazon Lex Runtime Service APIrequestsPostText  Sends user input \(text or SSML\) to Amazon Lex\. Client applications can use this API to send requests to Amazon Lex at runtime\. Amazon Lex then interprets the user input using the machine learning model it built for the bot\.   In response, Amazon Lex returns the next `message` to convey to the user an optional `responseCard` to display\. Consider the following example messages:     For a user input "I would like a pizza", Amazon Lex might return a response with a message eliciting slot data \(for example, PizzaSize\): "What size pizza would you like?"     After the user provides all of the pizza order information, Amazon Lex might return a response with a message to obtain user confirmation "Proceed with the pizza order?"\.     After the user replies to a confirmation prompt with a "yes", Amazon Lex might return a conclusion statement: "Thank you, your cheese pizza has been ordered\."\.     Not all Amazon Lex messages require a user response\. For example, a conclusion statement does not require a response\. Some messages require only a "yes" or "no" user response\. In addition to the `message`, Amazon Lex provides additional context about the message in the response that you might use to enhance client behavior, for example, to display the appropriate client user interface\. These are the `slotToElicit`, `dialogState`, `intentName`, and `slots` fields in the response\. Consider the following examples:    If the message is to elicit slot data, Amazon Lex returns the following context information:    `dialogState` set to ElicitSlot     `intentName` set to the intent name in the current context     `slotToElicit` set to the slot name for which the `message` is eliciting information     `slots` set to a map of slots, configured for the intent, with currently known values       If the message is a confirmation prompt, the `dialogState` is set to ConfirmIntent and `SlotToElicit` is set to null\.    If the message is a clarification prompt \(configured for the intent\) that indicates that user intent is not understood, the `dialogState` is set to ElicitIntent and `slotToElicit` is set to null\.     In addition, Amazon Lex also returns your application\-specific `sessionAttributes`\. For more information, see [Managing Conversation Context](http://docs.aws.amazon.com/lex/latest/dg/context-mgmt.html)\.   Request Syntax  

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
```   URI Request Parameters  The request requires the following URI parameters\.  

 ** botAlias **   
The alias of the Amazon Lex bot\. 

 ** botName **   
The name of the Amazon Lex bot\. 

 ** userId **   
The ID of the client application user\. Amazon Lex uses this to identify a user's conversation with your bot\. At runtime, each request must contain the `userID` field\.  
To decide the user ID to use for your application, consider the following factors\.  

+ The `userID` field must not contain any personally identifiable information of the user, for example, name, personal identification numbers, or other end user personal information\.

+ If you want a user to start a conversation on one device and continue on another device, use a user\-specific identifier\.

+ If you want the same user to be able to have two independent conversations on two different devices, choose a device\-specific identifier\.

+ A user can't have two independent conversations with two different versions of the same bot\. For example, a user can't have a conversation with the PROD and BETA versions of the same bot\. If you anticipate that a user will need to have conversation with two different versions, for example, while testing, include the bot alias in the user ID to separate the two conversations\.
Length Constraints: Minimum length of 2\. Maximum length of 100\.  
Pattern: `[0-9a-zA-Z._:-]+`     Request Body  The request accepts the following data in JSON format\.  

 ** inputText **   
The text that the user entered \(Amazon Lex interprets this text\)\.  
When you are using the AWS CLI, you can't pass a URL in the `--input-text` parameter\. Pass the URL using the `--cli-input-json` parameter instead\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 1024\.  
Required: Yes 

 ** requestAttributes **   
Request\-specific information passed between Amazon Lex and a client application\.  
The namespace `x-amz-lex:` is reserved for special attributes\. Don't create any request attributes with the prefix `x-amz-lex:`\.  
For more information, see [Setting Request Attributes](http://docs.aws.amazon.com/lex/latest/dg/context-mgmt.html#context-mgmt-request-attribs)\.  
Type: String to string map  
Required: No 

 ** sessionAttributes **   
Application\-specific information passed between Amazon Lex and a client application\.  
For more information, see [Setting Session Attributes](http://docs.aws.amazon.com/lex/latest/dg/context-mgmt.html#context-mgmt-session-attribs)\.  
Type: String to string map  
Required: No    Response Syntax  

```
HTTP/1.1 200
Content-type: application/json

{
   "dialogState": "string",
   "intentName": "string",
   "message": "string",
   "messageFormat": "string",
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
   "sessionAttributes": { 
      "string" : "string" 
   },
   "slots": { 
      "string" : "string" 
   },
   "slotToElicit": "string"
}
```   Response Elements  If the action is successful, the service sends back an HTTP 200 response\. The following data is returned in JSON format by the service\.  

 ** dialogState **   
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

 ** intentName **   
The current user intent that Amazon Lex is aware of\.  
Type: String 

 ** message **   
The message to convey to the user\. The message can come from the bot's configuration or from a Lambda function\.  
If the intent is not configured with a Lambda function, or if the Lambda function returned `Delegate` as the `dialogAction.type` its response, Amazon Lex decides on the next course of action and selects an appropriate message from the bot's configuration based on the current interaction context\. For example, if Amazon Lex isn't able to understand user input, it uses a clarification prompt message\.  
When you create an intent you can assign messages to groups\. When messages are assigned to groups Amazon Lex returns one message from each group in the response\. The message field is an escaped JSON string containing the messages\. For more information about the structure of the JSON string returned, see [Supported Message Formats](howitworks-manage-prompts.md#msg-prompts-formats)\.  
If the Lambda function returns a message, Amazon Lex passes it to the client in its response\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 1024\. 

 ** messageFormat **   
The format of the response message\. One of the following values:  

+  `PlainText` \- The message contains plain UTF\-8 text\.

+  `CustomPayload` \- The message is a custom format defined by the Lambda function\.

+  `SSML` \- The message contains text formatted for voice output\.

+  `Composite` \- The message contains an escaped JSON object containing one or more messages from the groups that messages were assigned to when the intent was created\.
Type: String  
Valid Values:` PlainText | CustomPayload | SSML | Composite`  

 ** responseCard **   
Represents the options that the user has to respond to the current prompt\. Response Card can come from the bot configuration \(in the Amazon Lex console, choose the settings button next to a slot\) or from a code hook \(Lambda function\)\.   
Type: [ResponseCard](API_runtime_ResponseCard.md) object 

 ** sessionAttributes **   
A map of key\-value pairs representing the session\-specific context information\.  
Type: String to string map 

 ** slots **   
 The intent slots that Amazon Lex detected from the user input in the conversation\.   
Amazon Lex creates a resolution list containing likely values for a slot\. The value that it returns is determined by the `valueSelectionStrategy` selected when the slot type was created or updated\. If `valueSelectionStrategy` is set to `ORIGINAL_VALUE`, the value provided by the user is returned, if the user value is similar to the slot values\. If `valueSelectionStrategy` is set to `TOP_RESOLUTION` Amazon Lex returns the first value in the resolution list or, if there is no resolution list, null\. If you don't specify a `valueSelectionStrategy`, the default is `ORIGINAL_VALUE`\.  
Type: String to string map 

 ** slotToElicit **   
If the `dialogState` value is `ElicitSlot`, returns the name of the slot for which Amazon Lex is eliciting a value\.   
Type: String    Errors   

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
HTTP Status Code: 404    See Also   For more information about using this API in one of the language\-specific AWS SDKs, see the following:    [AWS Command Line Interface](http://docs.aws.amazon.com/goto/aws-cli/runtime.lex-2016-11-28/PostText)     [AWS SDK for \.NET](http://docs.aws.amazon.com/goto/DotNetSDKV3/runtime.lex-2016-11-28/PostText)     [AWS SDK for C\+\+](http://docs.aws.amazon.com/goto/SdkForCpp/runtime.lex-2016-11-28/PostText)     [AWS SDK for Go](http://docs.aws.amazon.com/goto/SdkForGoV1/runtime.lex-2016-11-28/PostText)     [AWS SDK for Java](http://docs.aws.amazon.com/goto/SdkForJava/runtime.lex-2016-11-28/PostText)     [AWS SDK for JavaScript](http://docs.aws.amazon.com/goto/AWSJavaScriptSDK/runtime.lex-2016-11-28/PostText)     [AWS SDK for PHP V3](http://docs.aws.amazon.com/goto/SdkForPHPV3/runtime.lex-2016-11-28/PostText)     [AWS SDK for Python](http://docs.aws.amazon.com/goto/boto3/runtime.lex-2016-11-28/PostText)     [AWS SDK for Ruby V2](http://docs.aws.amazon.com/goto/SdkForRubyV2/runtime.lex-2016-11-28/PostText)    ](API_runtime_PostText.md) operation, or when you use the [ PostContent Service: Amazon Lex Runtime Service APIrequestsPostContent   Sends user input \(text or speech\) to Amazon Lex\. Clients use this API to send text and audio requests to Amazon Lex at runtime\. Amazon Lex interprets the user input using the machine learning model that it built for the bot\.  The `PostContent` operation supports audio input at 8kHz and 16kHz\. You can use 8kHz audio to achieve higher speech recognition accuracy in telephone audio applications\.   In response, Amazon Lex returns the next message to convey to the user\. Consider the following example messages:     For a user input "I would like a pizza," Amazon Lex might return a response with a message eliciting slot data \(for example, `PizzaSize`\): "What size pizza would you like?"\.     After the user provides all of the pizza order information, Amazon Lex might return a response with a message to get user confirmation: "Order the pizza?"\.     After the user replies "Yes" to the confirmation prompt, Amazon Lex might return a conclusion statement: "Thank you, your cheese pizza has been ordered\."\.     Not all Amazon Lex messages require a response from the user\. For example, conclusion statements do not require a response\. Some messages require only a yes or no response\. In addition to the `message`, Amazon Lex provides additional context about the message in the response that you can use to enhance client behavior, such as displaying the appropriate client user interface\. Consider the following examples:     If the message is to elicit slot data, Amazon Lex returns the following context information:     `x-amz-lex-dialog-state` header set to `ElicitSlot`     `x-amz-lex-intent-name` header set to the intent name in the current context     `x-amz-lex-slot-to-elicit` header set to the slot name for which the `message` is eliciting information     `x-amz-lex-slots` header set to a map of slots configured for the intent with their current values       If the message is a confirmation prompt, the `x-amz-lex-dialog-state` header is set to `Confirmation` and the `x-amz-lex-slot-to-elicit` header is omitted\.     If the message is a clarification prompt configured for the intent, indicating that the user intent is not understood, the `x-amz-dialog-state` header is set to `ElicitIntent` and the `x-amz-slot-to-elicit` header is omitted\.     In addition, Amazon Lex also returns your application\-specific `sessionAttributes`\. For more information, see [Managing Conversation Context](http://docs.aws.amazon.com/lex/latest/dg/context-mgmt.html)\.   Request Syntax  

```
POST /bot/botName/alias/botAlias/user/userId/content HTTP/1.1
x-amz-lex-session-attributes: sessionAttributes
x-amz-lex-request-attributes: requestAttributes
Content-Type: contentType
Accept: accept

inputStream
```   URI Request Parameters  The request requires the following URI parameters\.  

 ** accept **   
 You pass this value as the `Accept` HTTP header\.   
 The message Amazon Lex returns in the response can be either text or speech based on the `Accept` HTTP header value in the request\.   

+  If the value is `text/plain; charset=utf-8`, Amazon Lex returns text in the response\. 

+  If the value begins with `audio/`, Amazon Lex returns speech in the response\. Amazon Lex uses Amazon Polly to generate the speech \(using the configuration you specified in the `Accept` header\)\. For example, if you specify `audio/mpeg` as the value, Amazon Lex returns speech in the MPEG format\.

  The following are the accepted values:

  + audio/mpeg

  + audio/ogg

  + audio/pcm

  + text/plain; charset=utf\-8

  + audio/\* \(defaults to mpeg\) 

 ** botAlias **   
Alias of the Amazon Lex bot\. 

 ** botName **   
Name of the Amazon Lex bot\. 

 ** contentType **   
 You pass this value as the `Content-Type` HTTP header\.   
 Indicates the audio format or text\. The header value must start with one of the following prefixes:   

+ PCM format, audio data must be in little\-endian byte order\.

  + audio/l16; rate=16000; channels=1

  + audio/x\-l16; sample\-rate=16000; channel\-count=1

  + audio/lpcm; sample\-rate=8000; sample\-size\-bits=16; channel\-count=1; is\-big\-endian=false 

+ Opus format

  + audio/x\-cbr\-opus\-with\-preamble; preamble\-size=0; bit\-rate=256000; frame\-size\-milliseconds=4

+ Text format

  + text/plain; charset=utf\-8 

 ** requestAttributes **   
You pass this value as the `x-amz-lex-request-attributes` HTTP header\.  
Request\-specific information passed between Amazon Lex and a client application\. The value must be a JSON serialized and base64 encoded map with string keys and values\. The total size of the `requestAttributes` and `sessionAttributes` headers is limited to 12 KB\.  
The namespace `x-amz-lex:` is reserved for special attributes\. Don't create any request attributes with the prefix `x-amz-lex:`\.  
For more information, see [Setting Request Attributes](http://docs.aws.amazon.com/lex/latest/dg/context-mgmt.html#context-mgmt-request-attribs)\. 

 ** sessionAttributes **   
You pass this value as the `x-amz-lex-session-attributes` HTTP header\.  
Application\-specific information passed between Amazon Lex and a client application\. The value must be a JSON serialized and base64 encoded map with string keys and values\. The total size of the `sessionAttributes` and `requestAttributes` headers is limited to 12 KB\.  
For more information, see [Setting Session Attributes](http://docs.aws.amazon.com/lex/latest/dg/context-mgmt.html#context-mgmt-session-attribs)\. 

 ** userId **   
The ID of the client application user\. Amazon Lex uses this to identify a user's conversation with your bot\. At runtime, each request must contain the `userID` field\.  
To decide the user ID to use for your application, consider the following factors\.  

+ The `userID` field must not contain any personally identifiable information of the user, for example, name, personal identification numbers, or other end user personal information\.

+ If you want a user to start a conversation on one device and continue on another device, use a user\-specific identifier\.

+ If you want the same user to be able to have two independent conversations on two different devices, choose a device\-specific identifier\.

+ A user can't have two independent conversations with two different versions of the same bot\. For example, a user can't have a conversation with the PROD and BETA versions of the same bot\. If you anticipate that a user will need to have conversation with two different versions, for example, while testing, include the bot alias in the user ID to separate the two conversations\.
Length Constraints: Minimum length of 2\. Maximum length of 100\.  
Pattern: `[0-9a-zA-Z._:-]+`     Request Body  The request accepts the following binary data\.  

 ** inputStream **   
 User input in PCM or Opus audio format or text format as described in the `Content-Type` HTTP header\.   
You can stream audio data to Amazon Lex or you can create a local buffer that captures all of the audio data before sending\. In general, you get better performance if you stream audio data rather than buffering the data locally\.    Response Syntax  

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
x-amz-lex-input-transcript: inputTranscript

audioStream
```   Response Elements  If the action is successful, the service sends back an HTTP 200 response\. The response returns the following HTTP headers\.  

 ** contentType **   
Content type as specified in the `Accept` HTTP header in the request\. 

 ** dialogState **   
Identifies the current state of the user interaction\. Amazon Lex returns one of the following values as `dialogState`\. The client can optionally use this information to customize the user interface\.   

+  `ElicitIntent` \- Amazon Lex wants to elicit the user's intent\. Consider the following examples: 

   For example, a user might utter an intent \("I want to order a pizza"\)\. If Amazon Lex cannot infer the user intent from this utterance, it will return this dialog state\. 

+  `ConfirmIntent` \- Amazon Lex is expecting a "yes" or "no" response\. 

  For example, Amazon Lex wants user confirmation before fulfilling an intent\. Instead of a simple "yes" or "no" response, a user might respond with additional information\. For example, "yes, but make it a thick crust pizza" or "no, I want to order a drink\." Amazon Lex can process such additional information \(in these examples, update the crust type slot or change the intent from OrderPizza to OrderDrink\)\. 

+  `ElicitSlot` \- Amazon Lex is expecting the value of a slot for the current intent\. 

   For example, suppose that in the response Amazon Lex sends this message: "What size pizza would you like?"\. A user might reply with the slot value \(e\.g\., "medium"\)\. The user might also provide additional information in the response \(e\.g\., "medium thick crust pizza"\)\. Amazon Lex can process such additional information appropriately\. 

+  `Fulfilled` \- Conveys that the Lambda function has successfully fulfilled the intent\. 

+  `ReadyForFulfillment` \- Conveys that the client has to fulfill the request\. 

+  `Failed` \- Conveys that the conversation with the user failed\. 

   This can happen for various reasons, including that the user does not provide an appropriate response to prompts from the service \(you can configure how many times Amazon Lex can prompt a user for specific information\), or if the Lambda function fails to fulfill the intent\. 
Valid Values:` ElicitIntent | ConfirmIntent | ElicitSlot | Fulfilled | ReadyForFulfillment | Failed`  

 ** inputTranscript **   
The text used to process the request\.  
If the input was an audio stream, the `inputTranscript` field contains the text extracted from the audio stream\. This is the text that is actually processed to recognize intents and slot values\. You can use this information to determine if Amazon Lex is correctly processing the audio that you send\. 

 ** intentName **   
Current user intent that Amazon Lex is aware of\. 

 ** message **   
The message to convey to the user\. The message can come from the bot's configuration or from a Lambda function\.  
If the intent is not configured with a Lambda function, or if the Lambda function returned `Delegate` as the `dialogAction.type` its response, Amazon Lex decides on the next course of action and selects an appropriate message from the bot's configuration based on the current interaction context\. For example, if Amazon Lex isn't able to understand user input, it uses a clarification prompt message\.  
When you create an intent you can assign messages to groups\. When messages are assigned to groups Amazon Lex returns one message from each group in the response\. The message field is an escaped JSON string containing the messages\. For more information about the structure of the JSON string returned, see [Supported Message Formats](howitworks-manage-prompts.md#msg-prompts-formats)\.  
If the Lambda function returns a message, Amazon Lex passes it to the client in its response\.  
Length Constraints: Minimum length of 1\. Maximum length of 1024\. 

 ** messageFormat **   
The format of the response message\. One of the following values:  

+  `PlainText` \- The message contains plain UTF\-8 text\.

+  `CustomPayload` \- The message is a custom format for the client\.

+  `SSML` \- The message contains text formatted for voice output\.

+  `Composite` \- The message contains an escaped JSON object containing one or more messages from the groups that messages were assigned to when the intent was created\.
Valid Values:` PlainText | CustomPayload | SSML | Composite`  

 ** sessionAttributes **   
 Map of key/value pairs representing the session\-specific context information\.  

 ** slots **   
Map of zero or more intent slots \(name/value pairs\) Amazon Lex detected from the user input during the conversation\.  
Amazon Lex creates a resolution list containing likely values for a slot\. The value that it returns is determined by the `valueSelectionStrategy` selected when the slot type was created or updated\. If `valueSelectionStrategy` is set to `ORIGINAL_VALUE`, the value provided by the user is returned, if the user value is similar to the slot values\. If `valueSelectionStrategy` is set to `TOP_RESOLUTION` Amazon Lex returns the first value in the resolution list or, if there is no resolution list, null\. If you don't specify a `valueSelectionStrategy`, the default is `ORIGINAL_VALUE`\. 

 ** slotToElicit **   
 If the `dialogState` value is `ElicitSlot`, returns the name of the slot for which Amazon Lex is eliciting a value\.   The response returns the following as the HTTP body\.  

 ** audioStream **   
The prompt \(or statement\) to convey to the user\. This is based on the bot configuration and context\. For example, if Amazon Lex did not understand the user intent, it sends the `clarificationPrompt` configured for the bot\. If the intent requires confirmation before taking the fulfillment action, it sends the `confirmationPrompt`\. Another example: Suppose that the Lambda function successfully fulfilled the intent, and sent a message to convey to the user\. Then Amazon Lex sends that message in the response\.     Errors   

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

 **NotAcceptableException**   
The accept header in the request does not have a valid value\.  
HTTP Status Code: 406 

 **NotFoundException**   
The resource \(such as the Amazon Lex bot or an alias\) that is referred to is not found\.  
HTTP Status Code: 404 

 **RequestTimeoutException**   
The input speech is too long\.  
HTTP Status Code: 408 

 **UnsupportedMediaTypeException**   
The Content\-Type header \(`PostContent` API\) has an invalid value\.   
HTTP Status Code: 415    Example   Example 1   In this request, the URI identifies a bot \(Traffic\), bot version \($LATEST\), and end user name \(someuser\)\. The `Content-Type` header identifies the format of the audio in the body\. Amazon Lex also supports other formats\. To convert audio from one format to another, if necessary, you can use SoX open source software\. You specify the format in which you want to get the response by adding the `Accept` HTTP header\.   In the response, the `x-amz-lex-message` header shows the response that Amazon Lex returned\. The client can then send this response to the user\. The same message is sent in audio/MPEG format through chunked encoding \(as requested\)\.   Sample Request  

```
"POST /bot/Traffic/alias/$LATEST/user/someuser/content HTTP/1.1[\r][\n]"
"x-amz-lex-session-attributes: eyJ1c2VyTmFtZSI6IkJvYiJ9[\r][\n]"
"Content-Type: audio/x-l16; channel-count=1; sample-rate=16000f[\r][\n]"
"Accept: audio/mpeg[\r][\n]"
"Host: runtime.lex.us-east-1.amazonaws.com[\r][\n]"
"Authorization: AWS4-HMAC-SHA256 Credential=BLANKED_OUT/20161230/us-east-1/lex/aws4_request, 
SignedHeaders=accept;content-type;host;x-amz-content-sha256;x-amz-date;x-amz-lex-session-attributes, Signature=78ca5b54ea3f64a17ff7522de02cd90a9acd2365b45a9ce9b96ea105bb1c7ec2[\r][\n]"
"X-Amz-Date: 20161230T181426Z[\r][\n]"
"X-Amz-Content-Sha256: e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855[\r][\n]"
"Transfer-Encoding: chunked[\r][\n]"
"Connection: Keep-Alive[\r][\n]"
"User-Agent: Apache-HttpClient/4.5.x (Java/1.8.0_112)[\r][\n]"
"Accept-Encoding: gzip,deflate[\r][\n]"
"[\r][\n]"
"1000[\r][\n]"
"[0x7][0x0][0x7][0x0][\n]"
"[0x0][0x7][0x0][0xfc][0xff][\n]"
"[0x0][\n]"
…
```   Sample Response  

```
"HTTP/1.1 200 OK[\r][\n]"
"x-amzn-RequestId: cc8b34af-cebb-11e6-a35c-55f3a992f28d[\r][\n]"
"x-amz-lex-message: Sorry, can you repeat that?[\r][\n]"
"x-amz-lex-dialog-state: ElicitIntent[\r][\n]"
"x-amz-lex-session-attributes: eyJ1c2VyTmFtZSI6IkJvYiJ9[\r][\n]"
"Content-Type: audio/mpeg[\r][\n]"
"Transfer-Encoding: chunked[\r][\n]"
"Date: Fri, 30 Dec 2016 18:14:28 GMT[\r][\n]"
"[\r][\n]"               
"2000[\r][\n]"
"ID3[0x4][0x0][0x0][0x0][0x0][0x0]#TSSE[0x0][0x0][0x0][0xf][0x0][0x0][0x3]Lavf57.41.100[0x0][0x0][0x0][0x0][0x0][0x0][0x0][0x0][0x0][0x0][0x0][0xff][0xf3]`[0xc4][0x0][0x1b]{[0x8d][0xe8][0x1]C[0x18][0x1][0x0]J[0xe0]`b[0xdd][0xd1][0xb][0xfd][0x11][0xdf][0xfe]";[0xbb][0xbb][0x9f][0xee][0xee][0xee][0xee]|DDD/[0xff][0xff][0xff][0xff]www?D[0xf7]w^?[0xff][0xfa]h[0x88][0x85][0xfe][0x88][0x88][0x88][[0xa2]'[0xff][0xfa]"{[0x9f][0xe8][0x88]]D[0xeb][0xbb][0xbb][0xa2]!u[0xfd][0xdd][0xdf][0x88][0x94][0x0]F[0xef][0xa1]8[0x0][0x82]w[0x88]N[0x0][0x0][0x9b][0xbb][0xe8][0xe
…
```     See Also   For more information about using this API in one of the language\-specific AWS SDKs, see the following:    [AWS Command Line Interface](http://docs.aws.amazon.com/goto/aws-cli/runtime.lex-2016-11-28/PostContent)     [AWS SDK for \.NET](http://docs.aws.amazon.com/goto/DotNetSDKV3/runtime.lex-2016-11-28/PostContent)     [AWS SDK for C\+\+](http://docs.aws.amazon.com/goto/SdkForCpp/runtime.lex-2016-11-28/PostContent)     [AWS SDK for Go](http://docs.aws.amazon.com/goto/SdkForGoV1/runtime.lex-2016-11-28/PostContent)     [AWS SDK for Java](http://docs.aws.amazon.com/goto/SdkForJava/runtime.lex-2016-11-28/PostContent)     [AWS SDK for JavaScript](http://docs.aws.amazon.com/goto/AWSJavaScriptSDK/runtime.lex-2016-11-28/PostContent)     [AWS SDK for PHP V3](http://docs.aws.amazon.com/goto/SdkForPHPV3/runtime.lex-2016-11-28/PostContent)     [AWS SDK for Python](http://docs.aws.amazon.com/goto/boto3/runtime.lex-2016-11-28/PostContent)     [AWS SDK for Ruby V2](http://docs.aws.amazon.com/goto/SdkForRubyV2/runtime.lex-2016-11-28/PostContent)    ](API_runtime_PostContent.md) operation with the `Accept` header set to `text/plain;charset=utf8`, Amazon Lex supports messages in the following formats:

+ `PlainText`—The message contains plain UTF\-8 text\.

+ `SSML`—The message contains text formatted for voice output\.

+ `CustomPayload`—The message contains a custom format that you have created for your client\. You can define the payload to meet the needs of your application\.

+ `Composite`—The message is a collection of messages, one from each message group\. For more information about message groups, see [Message Groups](#message-groups)\.

By default, Amazon Lex returns any one of the messages defined for a particular prompt\. For example, if you define five messages to elicit a slot value, Amazon Lex chooses one of the messages randomly and returns it to the client\.

If you want Amazon Lex to return a specific type of message to the client in a run\-time request, set the `x-amzn-lex:accept-content-types` request parameter\. The response is limited to the type or types requested\. If there is more than one message of the specified type, Amazon Lex returns one at random\. For more information about the `x-amz-lex:accept-content-types` header, see [Setting the Response Type](context-mgmt.md#special-response)\.

## Message Groups<a name="message-groups"></a>

A *message group* is a set of suitable responses to a particular prompt\. Use message groups when you want your bot to dynamically build the responses in a conversation\. When Amazon Lex returns a response to the client application, it randomly chooses one message from each group\. You can create a maximum of five message groups for each response\. Each group can contain a maximum of five messages\. For examples of creating message groups in the console, see [Responses](#msg-prompts-response)\.

To create a message group, you can use the console or you can use the [PutBot](API_PutBot.md), [PutIntent](API_PutIntent.md), or [PutSlotType](API_PutSlotType.md) operations to assign a group number to a message\. If you don't create a message group, or if you create only one message group, Amazon Lex sends a single message in the `Message` field\. Client applications get multiple messages in a response only when you have created more than one message group in the console, or when you create more than one message group when you create or update an intent with the [PutIntent](API_PutIntent.md) operation\. 

When Amazon Lex sends a message from a group, the response's `Message` field contains an escaped JSON object that contains the messages\. The following example shows the contents of the `Message` field when it contains multiple messages\.

**Note**  
The example is formatted for readability\. A response doesn't contain carriage returns \(CR\)\.

```
{\"messages\":[
   {\"type\":\"PlainText\",\"group\":0,\"value\":\"Plain text\"},
   {\"type\":\"SSML\",\"group\":1,\"value\":\"SSML text\"},
   {\"type\":\"CustomPayload\",\"group\":2,\"value\":\"Custom payload\"}
]}
```

You can set the format of the messages\. The format can be one of the following:

+ PlainText—The message is in plain UTF\-8 text\.

+ SSML—The message is Speech Synthesis Markup Language \(SSML\)\.

+ CustomPayload—The message is in a custom format that you specified\.

To control the format of messages that the `PostContent` and `PostText` operations return in the `Message` field, set the `x-amz-lex:accept-content-types` request attribute\. For example, if you set the header to the following, you receive only plain text and SSML messages in the response:

```
x-amz-lex:accept-content-types: PlainText,SSML
```

If you request a specific message format and a message group doesn't contain that a message with that format, you get a `NoUsableMessageException` exception\. When you use a message group to group messages by type, don't use the `x-amz-lex:accept-content-types` header\.

For more information about the `x-amz-lex:accept-content-types` header, see [Setting the Response Type](context-mgmt.md#special-response)\.

## Response Cards<a name="msg-prompts-resp-card"></a>

A *response card* contains a set of appropriate responses to a prompt\. Use response cards to simplify interactions for your users and increase your bot's accuracy by reducing typographical errors in text interactions\. You can send a response card for each prompt that Amazon Lex sends to your client application\. You can use response cards with Facebook Messenger, Slack, Twilio, and your own client applications\.

For example, in a taxi application, you can configure an option in the response card for "Home" and set the value to the user's home address\. When the user selects this option, Amazon Lex receives the entire address as the input text\.

![\[An example response card.\]](http://docs.aws.amazon.com/lex/latest/dg/images/resp-console-5.png)

You can define a response card for the following prompts:

+ Conclusion statement

+ Confirmation prompt

+ Follow\-up prompt

+ Rejection statement

+ Slot type utterances

You can define only one response card for each prompt\. 

You configure response cards when you create an intent\. You can define a static response card at build time using the console or the [PutIntent](API_PutIntent.md) operation\. Or you can define a dynamic response card at runtime in a Lambda function\. If you define both static and dynamic response cards, the dynamic response card takes precedence\. 

Amazon Lex sends response cards in the format that the client understands\. It transforms response cards for Facebook Messenger, Slack, and Twilio\. For other clients, Amazon Lex sends a JSON structure in the [PostText](API_runtime_PostText.md) response\. For example, if the client is Facebook Messenger, Amazon Lex transforms the response card to a generic template\. For more information about Facebook Messenger generic templates, see [Generic Template](https://developers.facebook.com/docs/messenger-platform/send-api-reference/generic-template) on the Facebook website\. For an example of the JSON structure, see [Generating Response Cards Dynamically](#msg-prompts-resp-card-dynamic)\.

You can use response cards only with the [PostText](API_runtime_PostText.md) operation\. You can't use response cards with the [PostContent](API_runtime_PostContent.md) operation\. 

### Defining Static Response Cards<a name="msg-prompts-resp-card-static"></a>

Define static response cards with the [PutBot](API_PutBot.md) operation or the Amazon Lex console when you create an intent\. A static response card is defined at the same time as the intent\. Use a static response card when the responses are fixed\. Suppose that you are creating a bot with an intent that has a slot for flavor\. When defining the flavor slot, you specify prompts, as shown in the following console screenshot:

![\[The intent editor in the console.\]](http://docs.aws.amazon.com/lex/latest/dg/images/resp-console-10a.png)

When defining prompts, you can optionally associate a response card and define details with the [PutBot](API_PutBot.md) operation, or, in the Amazon Lex console, as shown in the following example:

![\[The console showing the response card editor.\]](http://docs.aws.amazon.com/lex/latest/dg/images/resp-console-20a.png)

Now suppose that you've integrated your bot with Facebook Messenger\. The user can click the buttons to choose a flavor, as shown in the following illustration:

![\[A response card in Facebook Messenger.\]](http://docs.aws.amazon.com/lex/latest/dg/images/resp-fb-exampleA.png)

To customize the content of a response card, you can refer to session attributes\. At runtime, Amazon Lex substitutes these references with appropriate values from the session attributes\. For more information, see [Setting Session Attributes](context-mgmt.md#context-mgmt-session-attribs)\. For an example, see [Example: Using a Response Card](ex-resp-card.md)\.

### Generating Response Cards Dynamically<a name="msg-prompts-resp-card-dynamic"></a>

To generate response cards dynamically at runtime, use the initialization and validation Lambda function for the intent\. Use a dynamic response card when the responses are determined at runtime in the Lambda function\. In response to user input, the Lambda function generates a response card and returns it in the `dialogAction` section of the response\. For more information, see [Response Format](lambda-input-response-format.md#using-lambda-response-format)\. 

The following is a partial response from a Lambda function that shows the `responseCard` element\. It generates a user experience similar to the one shown in the preceding section\.

```
responseCard: {
  "version": 1,
  "contentType": "application/vnd.amazonaws.card.generic",
  "genericAttachments": [
    {
      "title": "What Flavor?",
      "subtitle": "What flavor do you want?",
      "imageUrl": "Link to image",
      "attachmentLinkUrl": "Link to attachment",
      "buttons": [
        {
          "text": "Lemon",
          "value": "lemon"
        },
        {
          "text": "Raspberry",
          "value": "raspberry"
        },
        {
          "text": "Plain",
          "value": "plain"
        }
      ]
    }
  ]
}
```

For an example, see [Example Bot: ScheduleAppointment](ex1-sch-appt.md)\.