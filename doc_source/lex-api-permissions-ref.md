# Amazon Lex API Permissions: Actions, Resources, and Conditions Reference<a name="lex-api-permissions-ref"></a>

Use the following table as a reference when setting up [Access Control](auth-and-access-control.md#access-control) and writing a permissions policy that you can attach to an IAM identity \(an identity\-based policy\)\. The list includes each Amazon Lex API operation, the corresponding action for which you can grant permissions to perform the action, and the AWS resource for which you can grant the permissions\. You specify the actions in the policy's `Action` field, and you specify the resource value in the policy's `Resource` field\. 

To express conditions, you can use AWS\-wide condition keys in your Amazon Lex policies\. For a complete list of AWS\-wide keys, see [Available Keys](http://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements.html#AvailableKeys) in the *IAM User Guide*\. 

**Note**  
To specify an action, use the `lex:` prefix followed by the API operation name, for example, `lex:PostText`\.

If you see an expand arrow \(**↗**\) in the upper\-right corner of the table, you can open the table in a new window\. To close the window, choose the close button \(**X**\) in the lower\-right corner\.


**Amazon Lex API and Required Permissions for Actions**  

| Amazon Lex API Operations | Required Permissions \(API Actions\) | Resources | 
| --- | --- | --- | 
|   [CreateBotVersion](API_CreateBotVersion.md)   | lex:CreateBotVersion |  `arn:aws:lex:region:account-id:bot:bot-name:$LATEST`  | 
|   [CreateIntentVersion](API_CreateIntentVersion.md)   | lex:CreateIntentVersion |  `arn:aws:lex:region:account-id:intent:intent-name:$LATEST`  | 
|   [CreateSlotTypeVersion](API_CreateSlotTypeVersion.md)   | lex:CreateSlotTypeVersion |  `arn:aws:lex:region:account-id:slottype:slottype-name:$LATEST`  | 
|   [DeleteBot](API_DeleteBot.md)   | lex:DeleteBot |  `arn:aws:lex:region:account-id:bot:bot-name:*`  | 
|   [DeleteBotAlias](API_DeleteBotAlias.md)   | lex:DeleteBotAlias |  `arn:aws:lex:region:account-id:bot:bot-name:alias-name`  | 
|   [DeleteBotChannelAssociation](API_DeleteBotChannelAssociation.md)   | lex:DeleteBotChannelAssociation |  `arn:aws:lex:region:account-id:bot-channel:bot-name:alias-name:channel-name`  | 
|   [DeleteBotVersion](API_DeleteBotVersion.md)   | lex:DeleteBotVersion |  `arn:aws:lex:region:account-id:bot:bot-name:version`  | 
|   [DeleteIntent](API_DeleteIntent.md)   | lex:DeleteIntent |  `arn:aws:lex:region:account-id:intent:intent-name:*`  | 
|   [DeleteIntentVersion](API_DeleteIntentVersion.md)   | lex:DeleteIntentVersion |  `arn:aws:lex:region:account-id:intent:intent-name:version`  | 
|   [DeleteSlotType](API_DeleteSlotType.md)   | lex:DeleteSlotType |  `arn:aws:lex:region:account-id:slottype:slottype-name:*`  | 
|   [DeleteSlotTypeVersion](API_DeleteSlotTypeVersion.md)   | lex:DeleteSlotTypeVersion |  `arn:aws:lex:region:account-id:slottype:slottype-name:version`  | 
|  [DeleteUtterances](API_DeleteUtterances.md)   | lex:DeleteUtterances | `arn:aws:lex:region:account-id:bot:bot-name:*` | 
|   [GetBot](API_GetBot.md)   | lex:GetBot |  `arn:aws:lex:region:account-id:bot:bot-name:version`  | 
|   [GetBotAlias](API_GetBotAlias.md)   | lex:GetBotAlias |  `arn:aws:lex:region:account-id:bot:bot-name:alias-name`  | 
|   [GetBotAliases](API_GetBotAliases.md)   | lex:GetBotAliases |  `arn:aws:lex:region:account-id:bot:bot-name:*`  | 
|   [GetBotChannelAssociation](API_GetBotChannelAssociation.md)   | lex:GetBotChannelAssociation |  `arn:aws:lex:region:account-id:bot-channel:bot-name:alias-name:channel-name`  | 
|   [GetBotChannelAssociations](API_GetBotChannelAssociations.md)   | lex:GetBotChannelAssociations |  arn:aws:lex:region:account\-id:bot\-channel:bot\-name:alias\-name:\*  | 
|   [GetBots](API_GetBots.md)   | lex:GetBots |  `arn:aws:lex:region:account-id:bot:*`  | 
|   [GetBotVersions](API_GetBotVersions.md)   | lex:GetBotVersions |  `arn:aws:lex:region:account-id:bot:bot-name:*`  | 
|   [GetBuiltinIntent](API_GetBuiltinIntent.md)   | lex:GetBuiltinIntent |  \*  | 
|   [GetBuiltinIntents](API_GetBuiltinIntents.md)   | lex:GetBuiltinIntents |  \*  | 
|   [GetBuiltinSlotTypes](API_GetBuiltinSlotTypes.md)   | lex:GetBuiltinSlotTypes |  \*  | 
|   [GetExport](API_GetExport.md) \(see note\)   | lex:GetExport |  `arn:aws:lex:region:account-id:bot:bot-name:bot-version`  | 
|   [GetIntent](API_GetIntent.md)   | lex:GetIntent |  `arn:aws:lex:region:account-id:intent:intent-name:version`  | 
|   [GetIntents](API_GetIntents.md)   | lex:GetIntents |  `arn:aws:lex:region:account-id:intent:*`  | 
|   [GetIntentVersions](API_GetIntentVersions.md)   | lex:GetIntentVersions |  `arn:aws:lex:region:account-id:intent:intent-name:*`  | 
|   [GetSlotType](API_GetSlotType.md)   | lex:GetSlotType |  `arn:aws:lex:region:account-id:slottype:slottype-name:version`  | 
|   [GetSlotTypes](API_GetSlotTypes.md)   | lex:GetSlotTypes |  `arn:aws:lex:region:account-id:slottype:*`  | 
|   [GetSlotTypeVersions](API_GetSlotTypeVersions.md)   | lex:GetSlotTypeVersions |  `arn:aws:lex:region:account-id:slottype:slottype-name:*`  | 
| [GetUtterancesView](API_GetUtterancesView.md) | `lex:GetUtterancesView` | `arn:aws:lex:region:account-id:bot:bot-name:version` | 
|   [ PostContent Service: Amazon Lex Runtime Service APIrequestsPostContent   Sends user input \(text or speech\) to Amazon Lex\. Clients use this API to send text and audio requests to Amazon Lex at runtime\. Amazon Lex interprets the user input using the machine learning model that it built for the bot\.  The `PostContent` operation supports audio input at 8kHz and 16kHz\. You can use 8kHz audio to achieve higher speech recognition accuracy in telephone audio applications\.   In response, Amazon Lex returns the next message to convey to the user\. Consider the following example messages:     For a user input "I would like a pizza," Amazon Lex might return a response with a message eliciting slot data \(for example, `PizzaSize`\): "What size pizza would you like?"\.     After the user provides all of the pizza order information, Amazon Lex might return a response with a message to get user confirmation: "Order the pizza?"\.     After the user replies "Yes" to the confirmation prompt, Amazon Lex might return a conclusion statement: "Thank you, your cheese pizza has been ordered\."\.     Not all Amazon Lex messages require a response from the user\. For example, conclusion statements do not require a response\. Some messages require only a yes or no response\. In addition to the `message`, Amazon Lex provides additional context about the message in the response that you can use to enhance client behavior, such as displaying the appropriate client user interface\. Consider the following examples:     If the message is to elicit slot data, Amazon Lex returns the following context information:     `x-amz-lex-dialog-state` header set to `ElicitSlot`     `x-amz-lex-intent-name` header set to the intent name in the current context     `x-amz-lex-slot-to-elicit` header set to the slot name for which the `message` is eliciting information     `x-amz-lex-slots` header set to a map of slots configured for the intent with their current values       If the message is a confirmation prompt, the `x-amz-lex-dialog-state` header is set to `Confirmation` and the `x-amz-lex-slot-to-elicit` header is omitted\.     If the message is a clarification prompt configured for the intent, indicating that the user intent is not understood, the `x-amz-dialog-state` header is set to `ElicitIntent` and the `x-amz-slot-to-elicit` header is omitted\.     In addition, Amazon Lex also returns your application\-specific `sessionAttributes`\. For more information, see [Managing Conversation Context](http://docs.aws.amazon.com/lex/latest/dg/context-mgmt.html)\.   Request Syntax  

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
```     See Also   For more information about using this API in one of the language\-specific AWS SDKs, see the following:    [AWS Command Line Interface](http://docs.aws.amazon.com/goto/aws-cli/runtime.lex-2016-11-28/PostContent)     [AWS SDK for \.NET](http://docs.aws.amazon.com/goto/DotNetSDKV3/runtime.lex-2016-11-28/PostContent)     [AWS SDK for C\+\+](http://docs.aws.amazon.com/goto/SdkForCpp/runtime.lex-2016-11-28/PostContent)     [AWS SDK for Go](http://docs.aws.amazon.com/goto/SdkForGoV1/runtime.lex-2016-11-28/PostContent)     [AWS SDK for Java](http://docs.aws.amazon.com/goto/SdkForJava/runtime.lex-2016-11-28/PostContent)     [AWS SDK for JavaScript](http://docs.aws.amazon.com/goto/AWSJavaScriptSDK/runtime.lex-2016-11-28/PostContent)     [AWS SDK for PHP V3](http://docs.aws.amazon.com/goto/SdkForPHPV3/runtime.lex-2016-11-28/PostContent)     [AWS SDK for Python](http://docs.aws.amazon.com/goto/boto3/runtime.lex-2016-11-28/PostContent)     [AWS SDK for Ruby V2](http://docs.aws.amazon.com/goto/SdkForRubyV2/runtime.lex-2016-11-28/PostContent)    ](API_runtime_PostContent.md)   | lex:PostContent |  `arn:aws:lex:region:account-id:bot:bot-name:alias`  | 
|   [ PostText Service: Amazon Lex Runtime Service APIrequestsPostText  Sends user input \(text\-only\) to Amazon Lex\. Client applications can use this API to send requests to Amazon Lex at runtime\. Amazon Lex then interprets the user input using the machine learning model it built for the bot\.   In response, Amazon Lex returns the next `message` to convey to the user an optional `responseCard` to display\. Consider the following example messages:     For a user input "I would like a pizza", Amazon Lex might return a response with a message eliciting slot data \(for example, PizzaSize\): "What size pizza would you like?"     After the user provides all of the pizza order information, Amazon Lex might return a response with a message to obtain user confirmation "Proceed with the pizza order?"\.     After the user replies to a confirmation prompt with a "yes", Amazon Lex might return a conclusion statement: "Thank you, your cheese pizza has been ordered\."\.     Not all Amazon Lex messages require a user response\. For example, a conclusion statement does not require a response\. Some messages require only a "yes" or "no" user response\. In addition to the `message`, Amazon Lex provides additional context about the message in the response that you might use to enhance client behavior, for example, to display the appropriate client user interface\. These are the `slotToElicit`, `dialogState`, `intentName`, and `slots` fields in the response\. Consider the following examples:    If the message is to elicit slot data, Amazon Lex returns the following context information:    `dialogState` set to ElicitSlot     `intentName` set to the intent name in the current context     `slotToElicit` set to the slot name for which the `message` is eliciting information     `slots` set to a map of slots, configured for the intent, with currently known values       If the message is a confirmation prompt, the `dialogState` is set to ConfirmIntent and `SlotToElicit` is set to null\.    If the message is a clarification prompt \(configured for the intent\) that indicates that user intent is not understood, the `dialogState` is set to ElicitIntent and `slotToElicit` is set to null\.     In addition, Amazon Lex also returns your application\-specific `sessionAttributes`\. For more information, see [Managing Conversation Context](http://docs.aws.amazon.com/lex/latest/dg/context-mgmt.html)\.   Request Syntax  

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
HTTP Status Code: 404    See Also   For more information about using this API in one of the language\-specific AWS SDKs, see the following:    [AWS Command Line Interface](http://docs.aws.amazon.com/goto/aws-cli/runtime.lex-2016-11-28/PostText)     [AWS SDK for \.NET](http://docs.aws.amazon.com/goto/DotNetSDKV3/runtime.lex-2016-11-28/PostText)     [AWS SDK for C\+\+](http://docs.aws.amazon.com/goto/SdkForCpp/runtime.lex-2016-11-28/PostText)     [AWS SDK for Go](http://docs.aws.amazon.com/goto/SdkForGoV1/runtime.lex-2016-11-28/PostText)     [AWS SDK for Java](http://docs.aws.amazon.com/goto/SdkForJava/runtime.lex-2016-11-28/PostText)     [AWS SDK for JavaScript](http://docs.aws.amazon.com/goto/AWSJavaScriptSDK/runtime.lex-2016-11-28/PostText)     [AWS SDK for PHP V3](http://docs.aws.amazon.com/goto/SdkForPHPV3/runtime.lex-2016-11-28/PostText)     [AWS SDK for Python](http://docs.aws.amazon.com/goto/boto3/runtime.lex-2016-11-28/PostText)     [AWS SDK for Ruby V2](http://docs.aws.amazon.com/goto/SdkForRubyV2/runtime.lex-2016-11-28/PostText)    ](API_runtime_PostText.md)   | lex:PostText |  `arn:aws:lex:region:account-id:bot:bot-name:alias-name`  | 
|   [PutBot](API_PutBot.md)   | lex:PutBot |  `arn:aws:lex:region:account-id:bot:bot-name:$LATEST`  | 
|   [PutBotAlias](API_PutBotAlias.md)   | lex:PutBotAlias |  `arn:aws:lex:region:account-id:bot:bot-name:alias-name`  | 
|   [PutIntent](API_PutIntent.md)   | lex:PutIntent |  `arn:aws:lex:region:account-id:intent:intent-name:$LATEST`  | 
|   [PutSlotType](API_PutSlotType.md)   | lex:PutSlotType |  `arn:aws:lex:region:account-id:slottype:slottype-name:$LATEST`  | 

**Note**  
The `GetExport` function checks permission at the bot level and, if authorized, exports all relevant intent and slot type information associated with the specified bot\. GetExport does not check intent\-level and slot type\-level permissions\. 