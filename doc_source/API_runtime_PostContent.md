# PostContent<a name="API_runtime_PostContent"></a>

 Sends user input \(text or speech\) to Amazon Lex\. Clients use this API to send text and audio requests to Amazon Lex at runtime\. Amazon Lex interprets the user input using the machine learning model that it built for the bot\. 

The `PostContent` operation supports audio input at 8kHz and 16kHz\. You can use 8kHz audio to achieve higher speech recognition accuracy in telephone audio applications\. 

 In response, Amazon Lex returns the next message to convey to the user\. Consider the following example messages: 
+  For a user input "I would like a pizza," Amazon Lex might return a response with a message eliciting slot data \(for example, `PizzaSize`\): "What size pizza would you like?"\. 
+  After the user provides all of the pizza order information, Amazon Lex might return a response with a message to get user confirmation: "Order the pizza?"\. 
+  After the user replies "Yes" to the confirmation prompt, Amazon Lex might return a conclusion statement: "Thank you, your cheese pizza has been ordered\."\. 

 Not all Amazon Lex messages require a response from the user\. For example, conclusion statements do not require a response\. Some messages require only a yes or no response\. In addition to the `message`, Amazon Lex provides additional context about the message in the response that you can use to enhance client behavior, such as displaying the appropriate client user interface\. Consider the following examples: 
+  If the message is to elicit slot data, Amazon Lex returns the following context information: 
  +  `x-amz-lex-dialog-state` header set to `ElicitSlot` 
  +  `x-amz-lex-intent-name` header set to the intent name in the current context 
  +  `x-amz-lex-slot-to-elicit` header set to the slot name for which the `message` is eliciting information 
  +  `x-amz-lex-slots` header set to a map of slots configured for the intent with their current values 
+  If the message is a confirmation prompt, the `x-amz-lex-dialog-state` header is set to `Confirmation` and the `x-amz-lex-slot-to-elicit` header is omitted\. 
+  If the message is a clarification prompt configured for the intent, indicating that the user intent is not understood, the `x-amz-dialog-state` header is set to `ElicitIntent` and the `x-amz-slot-to-elicit` header is omitted\. 

 In addition, Amazon Lex also returns your application\-specific `sessionAttributes`\. For more information, see [Managing Conversation Context](https://docs.aws.amazon.com/lex/latest/dg/context-mgmt.html)\. 

## Request Syntax<a name="API_runtime_PostContent_RequestSyntax"></a>

```
POST /bot/botName/alias/botAlias/user/userId/content HTTP/1.1
x-amz-lex-session-attributes: sessionAttributes
x-amz-lex-request-attributes: requestAttributes
Content-Type: contentType
Accept: accept

inputStream
```

## URI Request Parameters<a name="API_runtime_PostContent_RequestParameters"></a>

The request uses the following URI parameters\.

 ** [accept](#API_runtime_PostContent_RequestSyntax) **   <a name="lex-runtime_PostContent-request-accept"></a>
 You pass this value as the `Accept` HTTP header\.   
 The message Amazon Lex returns in the response can be either text or speech based on the `Accept` HTTP header value in the request\.   
+  If the value is `text/plain; charset=utf-8`, Amazon Lex returns text in the response\. 
+  If the value begins with `audio/`, Amazon Lex returns speech in the response\. Amazon Lex uses Amazon Polly to generate the speech \(using the configuration you specified in the `Accept` header\)\. For example, if you specify `audio/mpeg` as the value, Amazon Lex returns speech in the MPEG format\.
+ If the value is `audio/pcm`, the speech returned is `audio/pcm` in 16\-bit, little endian format\. 
+ The following are the accepted values:
  + audio/mpeg
  + audio/ogg
  + audio/pcm
  + text/plain; charset=utf\-8
  + audio/\* \(defaults to mpeg\)

 ** [botAlias](#API_runtime_PostContent_RequestSyntax) **   <a name="lex-runtime_PostContent-request-botAlias"></a>
Alias of the Amazon Lex bot\.  
Required: Yes

 ** [botName](#API_runtime_PostContent_RequestSyntax) **   <a name="lex-runtime_PostContent-request-botName"></a>
Name of the Amazon Lex bot\.  
Required: Yes

 ** [contentType](#API_runtime_PostContent_RequestSyntax) **   <a name="lex-runtime_PostContent-request-contentType"></a>
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
Required: Yes

 ** [requestAttributes](#API_runtime_PostContent_RequestSyntax) **   <a name="lex-runtime_PostContent-request-requestAttributes"></a>
You pass this value as the `x-amz-lex-request-attributes` HTTP header\.  
Request\-specific information passed between Amazon Lex and a client application\. The value must be a JSON serialized and base64 encoded map with string keys and values\. The total size of the `requestAttributes` and `sessionAttributes` headers is limited to 12 KB\.  
The namespace `x-amz-lex:` is reserved for special attributes\. Don't create any request attributes with the prefix `x-amz-lex:`\.  
For more information, see [Setting Request Attributes](https://docs.aws.amazon.com/lex/latest/dg/context-mgmt.html#context-mgmt-request-attribs)\.

 ** [sessionAttributes](#API_runtime_PostContent_RequestSyntax) **   <a name="lex-runtime_PostContent-request-sessionAttributes"></a>
You pass this value as the `x-amz-lex-session-attributes` HTTP header\.  
Application\-specific information passed between Amazon Lex and a client application\. The value must be a JSON serialized and base64 encoded map with string keys and values\. The total size of the `sessionAttributes` and `requestAttributes` headers is limited to 12 KB\.  
For more information, see [Setting Session Attributes](https://docs.aws.amazon.com/lex/latest/dg/context-mgmt.html#context-mgmt-session-attribs)\.

 ** [userId](#API_runtime_PostContent_RequestSyntax) **   <a name="lex-runtime_PostContent-request-userId"></a>
The ID of the client application user\. Amazon Lex uses this to identify a user's conversation with your bot\. At runtime, each request must contain the `userID` field\.  
To decide the user ID to use for your application, consider the following factors\.  
+ The `userID` field must not contain any personally identifiable information of the user, for example, name, personal identification numbers, or other end user personal information\.
+ If you want a user to start a conversation on one device and continue on another device, use a user\-specific identifier\.
+ If you want the same user to be able to have two independent conversations on two different devices, choose a device\-specific identifier\.
+ A user can't have two independent conversations with two different versions of the same bot\. For example, a user can't have a conversation with the PROD and BETA versions of the same bot\. If you anticipate that a user will need to have conversation with two different versions, for example, while testing, include the bot alias in the user ID to separate the two conversations\.
Length Constraints: Minimum length of 2\. Maximum length of 100\.  
Pattern: `[0-9a-zA-Z._:-]+`   
Required: Yes

## Request Body<a name="API_runtime_PostContent_RequestBody"></a>

The request accepts the following binary data\.

 ** [inputStream](#API_runtime_PostContent_RequestSyntax) **   <a name="lex-runtime_PostContent-request-inputStream"></a>
 User input in PCM or Opus audio format or text format as described in the `Content-Type` HTTP header\.   
You can stream audio data to Amazon Lex or you can create a local buffer that captures all of the audio data before sending\. In general, you get better performance if you stream audio data rather than buffering the data locally\.  
Required: Yes

## Response Syntax<a name="API_runtime_PostContent_ResponseSyntax"></a>

```
HTTP/1.1 200
Content-Type: contentType
x-amz-lex-intent-name: intentName
x-amz-lex-nlu-intent-confidence: nluIntentConfidence
x-amz-lex-alternative-intents: alternativeIntents
x-amz-lex-slots: slots
x-amz-lex-session-attributes: sessionAttributes
x-amz-lex-sentiment: sentimentResponse
x-amz-lex-message: message
x-amz-lex-message-format: messageFormat
x-amz-lex-dialog-state: dialogState
x-amz-lex-slot-to-elicit: slotToElicit
x-amz-lex-input-transcript: inputTranscript
x-amz-lex-bot-version: botVersion
x-amz-lex-session-id: sessionId

audioStream
```

## Response Elements<a name="API_runtime_PostContent_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The response returns the following HTTP headers\.

 ** [alternativeIntents](#API_runtime_PostContent_ResponseSyntax) **   <a name="lex-runtime_PostContent-response-alternativeIntents"></a>
One to four alternative intents that may be applicable to the user's intent\.  
Each alternative includes a score that indicates how confident Amazon Lex is that the intent matches the user's intent\. The intents are sorted by the confidence score\.

 ** [botVersion](#API_runtime_PostContent_ResponseSyntax) **   <a name="lex-runtime_PostContent-response-botVersion"></a>
The version of the bot that responded to the conversation\. You can use this information to help determine if one version of a bot is performing better than another version\.  
If you have enabled the new natural language understanding \(NLU\) model, you can use this to determine if the improvement is due to changes to the bot or changes to the NLU\.  
For more information about enabling the new NLU, see the [enableModelImprovements](https://docs.aws.amazon.com/lex/latest/dg/API_PutBot.html#lex-PutBot-request-enableModelImprovements) parameter of the `PutBot` operation\.  
Length Constraints: Minimum length of 1\. Maximum length of 64\.  
Pattern: `[0-9]+|\$LATEST` 

 ** [contentType](#API_runtime_PostContent_ResponseSyntax) **   <a name="lex-runtime_PostContent-response-contentType"></a>
Content type as specified in the `Accept` HTTP header in the request\.

 ** [dialogState](#API_runtime_PostContent_ResponseSyntax) **   <a name="lex-runtime_PostContent-response-dialogState"></a>
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

 ** [inputTranscript](#API_runtime_PostContent_ResponseSyntax) **   <a name="lex-runtime_PostContent-response-inputTranscript"></a>
The text used to process the request\.  
If the input was an audio stream, the `inputTranscript` field contains the text extracted from the audio stream\. This is the text that is actually processed to recognize intents and slot values\. You can use this information to determine if Amazon Lex is correctly processing the audio that you send\.

 ** [intentName](#API_runtime_PostContent_ResponseSyntax) **   <a name="lex-runtime_PostContent-response-intentName"></a>
Current user intent that Amazon Lex is aware of\.

 ** [message](#API_runtime_PostContent_ResponseSyntax) **   <a name="lex-runtime_PostContent-response-message"></a>
The message to convey to the user\. The message can come from the bot's configuration or from a Lambda function\.  
If the intent is not configured with a Lambda function, or if the Lambda function returned `Delegate` as the `dialogAction.type` in its response, Amazon Lex decides on the next course of action and selects an appropriate message from the bot's configuration based on the current interaction context\. For example, if Amazon Lex isn't able to understand user input, it uses a clarification prompt message\.  
When you create an intent you can assign messages to groups\. When messages are assigned to groups Amazon Lex returns one message from each group in the response\. The message field is an escaped JSON string containing the messages\. For more information about the structure of the JSON string returned, see [Supported Message Formats](howitworks-manage-prompts.md#msg-prompts-formats)\.  
If the Lambda function returns a message, Amazon Lex passes it to the client in its response\.  
Length Constraints: Minimum length of 1\. Maximum length of 1024\.

 ** [messageFormat](#API_runtime_PostContent_ResponseSyntax) **   <a name="lex-runtime_PostContent-response-messageFormat"></a>
The format of the response message\. One of the following values:  
+  `PlainText` \- The message contains plain UTF\-8 text\.
+  `CustomPayload` \- The message is a custom format for the client\.
+  `SSML` \- The message contains text formatted for voice output\.
+  `Composite` \- The message contains an escaped JSON object containing one or more messages from the groups that messages were assigned to when the intent was created\.
Valid Values:` PlainText | CustomPayload | SSML | Composite` 

 ** [nluIntentConfidence](#API_runtime_PostContent_ResponseSyntax) **   <a name="lex-runtime_PostContent-response-nluIntentConfidence"></a>
Provides a score that indicates how confident Amazon Lex is that the returned intent is the one that matches the user's intent\. The score is between 0\.0 and 1\.0\.  
The score is a relative score, not an absolute score\. The score may change based on improvements to the Amazon Lex NLU\.

 ** [sentimentResponse](#API_runtime_PostContent_ResponseSyntax) **   <a name="lex-runtime_PostContent-response-sentimentResponse"></a>
The sentiment expressed in an utterance\.  
When the bot is configured to send utterances to Amazon Comprehend for sentiment analysis, this field contains the result of the analysis\.

 ** [sessionAttributes](#API_runtime_PostContent_ResponseSyntax) **   <a name="lex-runtime_PostContent-response-sessionAttributes"></a>
 Map of key/value pairs representing the session\-specific context information\. 

 ** [sessionId](#API_runtime_PostContent_ResponseSyntax) **   <a name="lex-runtime_PostContent-response-sessionId"></a>
The unique identifier for the session\.

 ** [slots](#API_runtime_PostContent_ResponseSyntax) **   <a name="lex-runtime_PostContent-response-slots"></a>
Map of zero or more intent slots \(name/value pairs\) Amazon Lex detected from the user input during the conversation\. The field is base\-64 encoded\.  
Amazon Lex creates a resolution list containing likely values for a slot\. The value that it returns is determined by the `valueSelectionStrategy` selected when the slot type was created or updated\. If `valueSelectionStrategy` is set to `ORIGINAL_VALUE`, the value provided by the user is returned, if the user value is similar to the slot values\. If `valueSelectionStrategy` is set to `TOP_RESOLUTION` Amazon Lex returns the first value in the resolution list or, if there is no resolution list, null\. If you don't specify a `valueSelectionStrategy`, the default is `ORIGINAL_VALUE`\.

 ** [slotToElicit](#API_runtime_PostContent_ResponseSyntax) **   <a name="lex-runtime_PostContent-response-slotToElicit"></a>
 If the `dialogState` value is `ElicitSlot`, returns the name of the slot for which Amazon Lex is eliciting a value\. 

The response returns the following as the HTTP body\.

 ** [audioStream](#API_runtime_PostContent_ResponseSyntax) **   <a name="lex-runtime_PostContent-response-audioStream"></a>
The prompt \(or statement\) to convey to the user\. This is based on the bot configuration and context\. For example, if Amazon Lex did not understand the user intent, it sends the `clarificationPrompt` configured for the bot\. If the intent requires confirmation before taking the fulfillment action, it sends the `confirmationPrompt`\. Another example: Suppose that the Lambda function successfully fulfilled the intent, and sent a message to convey to the user\. Then Amazon Lex sends that message in the response\. 

## Errors<a name="API_runtime_PostContent_Errors"></a>

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
HTTP Status Code: 415

## Example<a name="API_runtime_PostContent_Examples"></a>

### Example 1<a name="API_runtime_PostContent_Example_1"></a>

 In this request, the URI identifies a bot \(Traffic\), bot version \($LATEST\), and end user name \(someuser\)\. The `Content-Type` header identifies the format of the audio in the body\. Amazon Lex also supports other formats\. To convert audio from one format to another, if necessary, you can use SoX open source software\. You specify the format in which you want to get the response by adding the `Accept` HTTP header\. 

 In the response, the `x-amz-lex-message` header shows the response that Amazon Lex returned\. The client can then send this response to the user\. The same message is sent in audio/MPEG format through chunked encoding \(as requested\)\. 

#### Sample Request<a name="API_runtime_PostContent_Example_1_Request"></a>

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
```

#### Sample Response<a name="API_runtime_PostContent_Example_1_Response"></a>

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
```

## See Also<a name="API_runtime_PostContent_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/runtime.lex-2016-11-28/PostContent) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/runtime.lex-2016-11-28/PostContent) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/runtime.lex-2016-11-28/PostContent) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/runtime.lex-2016-11-28/PostContent) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/runtime.lex-2016-11-28/PostContent) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/runtime.lex-2016-11-28/PostContent) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/runtime.lex-2016-11-28/PostContent) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/runtime.lex-2016-11-28/PostContent) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/runtime.lex-2016-11-28/PostContent) 