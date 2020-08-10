# PutBot<a name="API_PutBot"></a>

Creates an Amazon Lex conversational bot or replaces an existing bot\. When you create or update a bot you are only required to specify a name, a locale, and whether the bot is directed toward children under age 13\. You can use this to add intents later, or to remove intents from an existing bot\. When you create a bot with the minimum information, the bot is created or updated but Amazon Lex returns the `` response `FAILED`\. You can build the bot after you add one or more intents\. For more information about Amazon Lex bots, see [Amazon Lex: How It Works](how-it-works.md)\. 

If you specify the name of an existing bot, the fields in the request replace the existing values in the `$LATEST` version of the bot\. Amazon Lex removes any fields that you don't provide values for in the request, except for the `idleTTLInSeconds` and `privacySettings` fields, which are set to their default values\. If you don't specify values for required fields, Amazon Lex throws an exception\.

This operation requires permissions for the `lex:PutBot` action\. For more information, see [Identity and Access Management for Amazon Lex](security-iam.md)\.

## Request Syntax<a name="API_PutBot_RequestSyntax"></a>

```
PUT /bots/name/versions/$LATEST HTTP/1.1
Content-type: application/json

{
   "abortStatement": { 
      "messages": [ 
         { 
            "content": "string",
            "contentType": "string",
            "groupNumber": number
         }
      ],
      "responseCard": "string"
   },
   "checksum": "string",
   "childDirected": boolean,
   "clarificationPrompt": { 
      "maxAttempts": number,
      "messages": [ 
         { 
            "content": "string",
            "contentType": "string",
            "groupNumber": number
         }
      ],
      "responseCard": "string"
   },
   "createVersion": boolean,
   "description": "string",
   "detectSentiment": boolean,
   "enableModelImprovements": boolean,
   "idleSessionTTLInSeconds": number,
   "intents": [ 
      { 
         "intentName": "string",
         "intentVersion": "string"
      }
   ],
   "locale": "string",
   "nluIntentConfidenceThreshold": number,
   "processBehavior": "string",
   "tags": [ 
      { 
         "key": "string",
         "value": "string"
      }
   ],
   "voiceId": "string"
}
```

## URI Request Parameters<a name="API_PutBot_RequestParameters"></a>

The request uses the following URI parameters\.

 ** [name](#API_PutBot_RequestSyntax) **   <a name="lex-PutBot-request-name"></a>
The name of the bot\. The name is *not* case sensitive\.   
Length Constraints: Minimum length of 2\. Maximum length of 50\.  
Pattern: `^([A-Za-z]_?)+$`   
Required: Yes

## Request Body<a name="API_PutBot_RequestBody"></a>

The request accepts the following data in JSON format\.

 ** [abortStatement](#API_PutBot_RequestSyntax) **   <a name="lex-PutBot-request-abortStatement"></a>
When Amazon Lex can't understand the user's input in context, it tries to elicit the information a few times\. After that, Amazon Lex sends the message defined in `abortStatement` to the user, and then cancels the conversation\. To set the number of retries, use the `valueElicitationPrompt` field for the slot type\.   
For example, in a pizza ordering bot, Amazon Lex might ask a user "What type of crust would you like?" If the user's response is not one of the expected responses \(for example, "thin crust, "deep dish," etc\.\), Amazon Lex tries to elicit a correct response a few more times\.   
For example, in a pizza ordering application, `OrderPizza` might be one of the intents\. This intent might require the `CrustType` slot\. You specify the `valueElicitationPrompt` field when you create the `CrustType` slot\.  
If you have defined a fallback intent the cancel statement will not be sent to the user, the fallback intent is used instead\. For more information, see [ AMAZON\.FallbackIntent](https://docs.aws.amazon.com/lex/latest/dg/built-in-intent-fallback.html)\.  
Type: [Statement](API_Statement.md) object  
Required: No

 ** [checksum](#API_PutBot_RequestSyntax) **   <a name="lex-PutBot-request-checksum"></a>
Identifies a specific revision of the `$LATEST` version\.  
When you create a new bot, leave the `checksum` field blank\. If you specify a checksum you get a `BadRequestException` exception\.  
When you want to update a bot, set the `checksum` field to the checksum of the most recent revision of the `$LATEST` version\. If you don't specify the ` checksum` field, or if the checksum does not match the `$LATEST` version, you get a `PreconditionFailedException` exception\.  
Type: String  
Required: No

 ** [childDirected](#API_PutBot_RequestSyntax) **   <a name="lex-PutBot-request-childDirected"></a>
For each Amazon Lex bot created with the Amazon Lex Model Building Service, you must specify whether your use of Amazon Lex is related to a website, program, or other application that is directed or targeted, in whole or in part, to children under age 13 and subject to the Children's Online Privacy Protection Act \(COPPA\) by specifying `true` or `false` in the `childDirected` field\. By specifying `true` in the `childDirected` field, you confirm that your use of Amazon Lex **is** related to a website, program, or other application that is directed or targeted, in whole or in part, to children under age 13 and subject to COPPA\. By specifying `false` in the `childDirected` field, you confirm that your use of Amazon Lex **is not** related to a website, program, or other application that is directed or targeted, in whole or in part, to children under age 13 and subject to COPPA\. You may not specify a default value for the `childDirected` field that does not accurately reflect whether your use of Amazon Lex is related to a website, program, or other application that is directed or targeted, in whole or in part, to children under age 13 and subject to COPPA\.  
If your use of Amazon Lex relates to a website, program, or other application that is directed in whole or in part, to children under age 13, you must obtain any required verifiable parental consent under COPPA\. For information regarding the use of Amazon Lex in connection with websites, programs, or other applications that are directed or targeted, in whole or in part, to children under age 13, see the [Amazon Lex FAQ\.](https://aws.amazon.com/lex/faqs#data-security)   
Type: Boolean  
Required: Yes

 ** [clarificationPrompt](#API_PutBot_RequestSyntax) **   <a name="lex-PutBot-request-clarificationPrompt"></a>
When Amazon Lex doesn't understand the user's intent, it uses this message to get clarification\. To specify how many times Amazon Lex should repeat the clarification prompt, use the `maxAttempts` field\. If Amazon Lex still doesn't understand, it sends the message in the `abortStatement` field\.   
When you create a clarification prompt, make sure that it suggests the correct response from the user\. for example, for a bot that orders pizza and drinks, you might create this clarification prompt: "What would you like to do? You can say 'Order a pizza' or 'Order a drink\.'"  
If you have defined a fallback intent, it will be invoked if the clarification prompt is repeated the number of times defined in the `maxAttempts` field\. For more information, see [ AMAZON\.FallbackIntent](https://docs.aws.amazon.com/lex/latest/dg/built-in-intent-fallback.html)\.  
If you don't define a clarification prompt, at runtime Amazon Lex will return a 400 Bad Request exception in three cases:   
+ Follow\-up prompt \- When the user responds to a follow\-up prompt but does not provide an intent\. For example, in response to a follow\-up prompt that says "Would you like anything else today?" the user says "Yes\." Amazon Lex will return a 400 Bad Request exception because it does not have a clarification prompt to send to the user to get an intent\.
+ Lambda function \- When using a Lambda function, you return an `ElicitIntent` dialog type\. Since Amazon Lex does not have a clarification prompt to get an intent from the user, it returns a 400 Bad Request exception\.
+ PutSession operation \- When using the `PutSession` operation, you send an `ElicitIntent` dialog type\. Since Amazon Lex does not have a clarification prompt to get an intent from the user, it returns a 400 Bad Request exception\.
Type: [Prompt](API_Prompt.md) object  
Required: No

 ** [createVersion](#API_PutBot_RequestSyntax) **   <a name="lex-PutBot-request-createVersion"></a>
When set to `true` a new numbered version of the bot is created\. This is the same as calling the `CreateBotVersion` operation\. If you don't specify `createVersion`, the default is `false`\.  
Type: Boolean  
Required: No

 ** [description](#API_PutBot_RequestSyntax) **   <a name="lex-PutBot-request-description"></a>
A description of the bot\.  
Type: String  
Length Constraints: Minimum length of 0\. Maximum length of 200\.  
Required: No

 ** [detectSentiment](#API_PutBot_RequestSyntax) **   <a name="lex-PutBot-request-detectSentiment"></a>
When set to `true` user utterances are sent to Amazon Comprehend for sentiment analysis\. If you don't specify `detectSentiment`, the default is `false`\.  
Type: Boolean  
Required: No

 ** [enableModelImprovements](#API_PutBot_RequestSyntax) **   <a name="lex-PutBot-request-enableModelImprovements"></a>
Set to `true` to enable the use of a new natural language understanding \(NLU\) model\. Using the new NLU may improve the performance of your bot\.   
When you set the `enableModelImprovements` parameter to `true` you can use the `nluIntentConfidenceThreshold` parameter to configure confidence scores\. For more information, see [Confidence Scores](https://docs.aws.amazon.com/lex/latest/dg/confidence-scores.html)\.  
You can only set the `enableModelImprovements` parameter in certain Regions\. If you set the parameter to `true`, your bot will use the new NLU\. If you set the parameter to `false`, your bot will continue to use the original NLU\. If you set the parameter to `false` after setting it to `true`, your bot will return to the original NLU\.  
The Regions where you can set the `enableModelImprovements` parameter to `true` are:  
+ US East \(N\. Virginia\) \(us\-east\-1\)
+ US West \(Oregon\) \(us\-west\-2\)
+ EU \(Ireland\) \(eu\-west\-1\)
In other Regions, the `enableModelImprovements` parameter is set to `true` by default\. In these Regions setting the parameter to `false` throws a `ValidationException` exception\.  
+ Asia Pacific \(Singapore\) \(ap\-southeast\-1\)
+ Asia Pacific \(Sydney\) \(ap\-southeast\-2\)
+ Asia Pacific \(Tokyo\) \(ap\-northeast\-1\)
+ EU \(Frankfurt\) \(eu\-central\-1\)
+ EU \(London\) \(eu\-west\-2\)
Type: Boolean  
Required: No

 ** [idleSessionTTLInSeconds](#API_PutBot_RequestSyntax) **   <a name="lex-PutBot-request-idleSessionTTLInSeconds"></a>
The maximum time in seconds that Amazon Lex retains the data gathered in a conversation\.  
A user interaction session remains active for the amount of time specified\. If no conversation occurs during this time, the session expires and Amazon Lex deletes any data provided before the timeout\.  
For example, suppose that a user chooses the OrderPizza intent, but gets sidetracked halfway through placing an order\. If the user doesn't complete the order within the specified time, Amazon Lex discards the slot information that it gathered, and the user must start over\.  
If you don't include the `idleSessionTTLInSeconds` element in a `PutBot` operation request, Amazon Lex uses the default value\. This is also true if the request replaces an existing bot\.  
The default is 300 seconds \(5 minutes\)\.  
Type: Integer  
Valid Range: Minimum value of 60\. Maximum value of 86400\.  
Required: No

 ** [intents](#API_PutBot_RequestSyntax) **   <a name="lex-PutBot-request-intents"></a>
An array of `Intent` objects\. Each intent represents a command that a user can express\. For example, a pizza ordering bot might support an OrderPizza intent\. For more information, see [Amazon Lex: How It Works](how-it-works.md)\.  
Type: Array of [Intent](API_Intent.md) objects  
Required: No

 ** [locale](#API_PutBot_RequestSyntax) **   <a name="lex-PutBot-request-locale"></a>
 Specifies the target locale for the bot\. Any intent used in the bot must be compatible with the locale of the bot\.   
The default is `en-US`\.  
Type: String  
Valid Values:` en-US | en-GB | de-DE`   
Required: Yes

 ** [nluIntentConfidenceThreshold](#API_PutBot_RequestSyntax) **   <a name="lex-PutBot-request-nluIntentConfidenceThreshold"></a>
Determines the threshold where Amazon Lex will insert the `AMAZON.FallbackIntent`, `AMAZON.KendraSearchIntent`, or both when returning alternative intents in a [PostContent](https://docs.aws.amazon.com/lex/latest/dg/API_runtime_PostContent.html) or [PostText](https://docs.aws.amazon.com/lex/latest/dg/API_runtime_PostText.html) response\. `AMAZON.FallbackIntent` and `AMAZON.KendraSearchIntent` are only inserted if they are configured for the bot\.  
You must set the `enableModelImprovements` parameter to `true` to use confidence scores\.  
For example, suppose a bot is configured with the confidence threshold of 0\.80 and the `AMAZON.FallbackIntent`\. Amazon Lex returns three alternative intents with the following confidence scores: IntentA \(0\.70\), IntentB \(0\.60\), IntentC \(0\.50\)\. The response from the `PostText` operation would be:  
+ AMAZON\.FallbackIntent
+ IntentA
+ IntentB
+ IntentC
Type: Double  
Valid Range: Minimum value of 0\. Maximum value of 1\.  
Required: No

 ** [processBehavior](#API_PutBot_RequestSyntax) **   <a name="lex-PutBot-request-processBehavior"></a>
If you set the `processBehavior` element to `BUILD`, Amazon Lex builds the bot so that it can be run\. If you set the element to `SAVE` Amazon Lex saves the bot, but doesn't build it\.   
If you don't specify this value, the default value is `BUILD`\.  
Type: String  
Valid Values:` SAVE | BUILD`   
Required: No

 ** [tags](#API_PutBot_RequestSyntax) **   <a name="lex-PutBot-request-tags"></a>
A list of tags to add to the bot\. You can only add tags when you create a bot, you can't use the `PutBot` operation to update the tags on a bot\. To update tags, use the `TagResource` operation\.  
Type: Array of [Tag](API_Tag.md) objects  
Array Members: Minimum number of 0 items\. Maximum number of 200 items\.  
Required: No

 ** [voiceId](#API_PutBot_RequestSyntax) **   <a name="lex-PutBot-request-voiceId"></a>
The Amazon Polly voice ID that you want Amazon Lex to use for voice interactions with the user\. The locale configured for the voice must match the locale of the bot\. For more information, see [Voices in Amazon Polly](https://docs.aws.amazon.com/polly/latest/dg/voicelist.html) in the *Amazon Polly Developer Guide*\.  
Type: String  
Required: No

## Response Syntax<a name="API_PutBot_ResponseSyntax"></a>

```
HTTP/1.1 200
Content-type: application/json

{
   "abortStatement": { 
      "messages": [ 
         { 
            "content": "string",
            "contentType": "string",
            "groupNumber": number
         }
      ],
      "responseCard": "string"
   },
   "checksum": "string",
   "childDirected": boolean,
   "clarificationPrompt": { 
      "maxAttempts": number,
      "messages": [ 
         { 
            "content": "string",
            "contentType": "string",
            "groupNumber": number
         }
      ],
      "responseCard": "string"
   },
   "createdDate": number,
   "createVersion": boolean,
   "description": "string",
   "detectSentiment": boolean,
   "enableModelImprovements": boolean,
   "failureReason": "string",
   "idleSessionTTLInSeconds": number,
   "intents": [ 
      { 
         "intentName": "string",
         "intentVersion": "string"
      }
   ],
   "lastUpdatedDate": number,
   "locale": "string",
   "name": "string",
   "nluIntentConfidenceThreshold": number,
   "status": "string",
   "tags": [ 
      { 
         "key": "string",
         "value": "string"
      }
   ],
   "version": "string",
   "voiceId": "string"
}
```

## Response Elements<a name="API_PutBot_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [abortStatement](#API_PutBot_ResponseSyntax) **   <a name="lex-PutBot-response-abortStatement"></a>
The message that Amazon Lex uses to cancel a conversation\. For more information, see [PutBot](#API_PutBot)\.  
Type: [Statement](API_Statement.md) object

 ** [checksum](#API_PutBot_ResponseSyntax) **   <a name="lex-PutBot-response-checksum"></a>
Checksum of the bot that you created\.  
Type: String

 ** [childDirected](#API_PutBot_ResponseSyntax) **   <a name="lex-PutBot-response-childDirected"></a>
For each Amazon Lex bot created with the Amazon Lex Model Building Service, you must specify whether your use of Amazon Lex is related to a website, program, or other application that is directed or targeted, in whole or in part, to children under age 13 and subject to the Children's Online Privacy Protection Act \(COPPA\) by specifying `true` or `false` in the `childDirected` field\. By specifying `true` in the `childDirected` field, you confirm that your use of Amazon Lex **is** related to a website, program, or other application that is directed or targeted, in whole or in part, to children under age 13 and subject to COPPA\. By specifying `false` in the `childDirected` field, you confirm that your use of Amazon Lex **is not** related to a website, program, or other application that is directed or targeted, in whole or in part, to children under age 13 and subject to COPPA\. You may not specify a default value for the `childDirected` field that does not accurately reflect whether your use of Amazon Lex is related to a website, program, or other application that is directed or targeted, in whole or in part, to children under age 13 and subject to COPPA\.  
If your use of Amazon Lex relates to a website, program, or other application that is directed in whole or in part, to children under age 13, you must obtain any required verifiable parental consent under COPPA\. For information regarding the use of Amazon Lex in connection with websites, programs, or other applications that are directed or targeted, in whole or in part, to children under age 13, see the [Amazon Lex FAQ\.](https://aws.amazon.com/lex/faqs#data-security)   
Type: Boolean

 ** [clarificationPrompt](#API_PutBot_ResponseSyntax) **   <a name="lex-PutBot-response-clarificationPrompt"></a>
 The prompts that Amazon Lex uses when it doesn't understand the user's intent\. For more information, see [PutBot](#API_PutBot)\.   
Type: [Prompt](API_Prompt.md) object

 ** [createdDate](#API_PutBot_ResponseSyntax) **   <a name="lex-PutBot-response-createdDate"></a>
The date that the bot was created\.  
Type: Timestamp

 ** [createVersion](#API_PutBot_ResponseSyntax) **   <a name="lex-PutBot-response-createVersion"></a>
 `True` if a new version of the bot was created\. If the `createVersion` field was not specified in the request, the `createVersion` field is set to false in the response\.  
Type: Boolean

 ** [description](#API_PutBot_ResponseSyntax) **   <a name="lex-PutBot-response-description"></a>
A description of the bot\.  
Type: String  
Length Constraints: Minimum length of 0\. Maximum length of 200\.

 ** [detectSentiment](#API_PutBot_ResponseSyntax) **   <a name="lex-PutBot-response-detectSentiment"></a>
 `true` if the bot is configured to send user utterances to Amazon Comprehend for sentiment analysis\. If the `detectSentiment` field was not specified in the request, the `detectSentiment` field is `false` in the response\.  
Type: Boolean

 ** [enableModelImprovements](#API_PutBot_ResponseSyntax) **   <a name="lex-PutBot-response-enableModelImprovements"></a>
Indicates whether the bot uses the new natural language understanding \(NLU\) model or the original NLU\. True indicates that the bot is using the new model, otherwise, false\.  
Type: Boolean

 ** [failureReason](#API_PutBot_ResponseSyntax) **   <a name="lex-PutBot-response-failureReason"></a>
If `status` is `FAILED`, Amazon Lex provides the reason that it failed to build the bot\.  
Type: String

 ** [idleSessionTTLInSeconds](#API_PutBot_ResponseSyntax) **   <a name="lex-PutBot-response-idleSessionTTLInSeconds"></a>
The maximum length of time that Amazon Lex retains the data gathered in a conversation\. For more information, see [PutBot](#API_PutBot)\.  
Type: Integer  
Valid Range: Minimum value of 60\. Maximum value of 86400\.

 ** [intents](#API_PutBot_ResponseSyntax) **   <a name="lex-PutBot-response-intents"></a>
An array of `Intent` objects\. For more information, see [PutBot](#API_PutBot)\.  
Type: Array of [Intent](API_Intent.md) objects

 ** [lastUpdatedDate](#API_PutBot_ResponseSyntax) **   <a name="lex-PutBot-response-lastUpdatedDate"></a>
The date that the bot was updated\. When you create a resource, the creation date and last updated date are the same\.  
Type: Timestamp

 ** [locale](#API_PutBot_ResponseSyntax) **   <a name="lex-PutBot-response-locale"></a>
 The target locale for the bot\.   
Type: String  
Valid Values:` en-US | en-GB | de-DE` 

 ** [name](#API_PutBot_ResponseSyntax) **   <a name="lex-PutBot-response-name"></a>
The name of the bot\.  
Type: String  
Length Constraints: Minimum length of 2\. Maximum length of 50\.  
Pattern: `^([A-Za-z]_?)+$` 

 ** [nluIntentConfidenceThreshold](#API_PutBot_ResponseSyntax) **   <a name="lex-PutBot-response-nluIntentConfidenceThreshold"></a>
The score that determines where Amazon Lex inserts the `AMAZON.FallbackIntent`, `AMAZON.KendraSearchIntent`, or both when returning alternative intents in a [PostContent](https://docs.aws.amazon.com/lex/latest/dg/API_runtime_PostContent.html) or [PostText](https://docs.aws.amazon.com/lex/latest/dg/API_runtime_PostText.html) response\. `AMAZON.FallbackIntent` is inserted if the confidence score for all intents is below this value\. `AMAZON.KendraSearchIntent` is only inserted if it is configured for the bot\.  
Type: Double  
Valid Range: Minimum value of 0\. Maximum value of 1\.

 ** [status](#API_PutBot_ResponseSyntax) **   <a name="lex-PutBot-response-status"></a>
 When you send a request to create a bot with `processBehavior` set to `BUILD`, Amazon Lex sets the `status` response element to `BUILDING`\.  
In the `READY_BASIC_TESTING` state you can test the bot with user inputs that exactly match the utterances configured for the bot's intents and values in the slot types\.  
If Amazon Lex can't build the bot, Amazon Lex sets `status` to `FAILED`\. Amazon Lex returns the reason for the failure in the `failureReason` response element\.   
When you set `processBehavior` to `SAVE`, Amazon Lex sets the status code to `NOT BUILT`\.  
When the bot is in the `READY` state you can test and publish the bot\.  
Type: String  
Valid Values:` BUILDING | READY | READY_BASIC_TESTING | FAILED | NOT_BUILT` 

 ** [tags](#API_PutBot_ResponseSyntax) **   <a name="lex-PutBot-response-tags"></a>
A list of tags associated with the bot\.  
Type: Array of [Tag](API_Tag.md) objects  
Array Members: Minimum number of 0 items\. Maximum number of 200 items\.

 ** [version](#API_PutBot_ResponseSyntax) **   <a name="lex-PutBot-response-version"></a>
The version of the bot\. For a new bot, the version is always `$LATEST`\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 64\.  
Pattern: `\$LATEST|[0-9]+` 

 ** [voiceId](#API_PutBot_ResponseSyntax) **   <a name="lex-PutBot-response-voiceId"></a>
The Amazon Polly voice ID that Amazon Lex uses for voice interaction with the user\. For more information, see [PutBot](#API_PutBot)\.  
Type: String

## Errors<a name="API_PutBot_Errors"></a>

 **BadRequestException**   
The request is not well formed\. For example, a value is invalid or a required field is missing\. Check the field values, and try again\.  
HTTP Status Code: 400

 **ConflictException**   
 There was a conflict processing the request\. Try your request again\.   
HTTP Status Code: 409

 **InternalFailureException**   
An internal Amazon Lex error occurred\. Try your request again\.  
HTTP Status Code: 500

 **LimitExceededException**   
The request exceeded a limit\. Try your request again\.  
HTTP Status Code: 429

 **PreconditionFailedException**   
 The checksum of the resource that you are trying to change does not match the checksum in the request\. Check the resource's checksum and try again\.  
HTTP Status Code: 412

## See Also<a name="API_PutBot_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/lex-models-2017-04-19/PutBot) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/lex-models-2017-04-19/PutBot) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/lex-models-2017-04-19/PutBot) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/lex-models-2017-04-19/PutBot) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/lex-models-2017-04-19/PutBot) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/lex-models-2017-04-19/PutBot) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/lex-models-2017-04-19/PutBot) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/lex-models-2017-04-19/PutBot) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/lex-models-2017-04-19/PutBot) 