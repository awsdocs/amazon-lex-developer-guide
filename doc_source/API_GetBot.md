# GetBot<a name="API_GetBot"></a>

Returns metadata information for a specific bot\. You must provide the bot name and the bot version or alias\. 

 This operation requires permissions for the `lex:GetBot` action\. 

## Request Syntax<a name="API_GetBot_RequestSyntax"></a>

```
GET /bots/name/versions/versionoralias HTTP/1.1
```

## URI Request Parameters<a name="API_GetBot_RequestParameters"></a>

The request uses the following URI parameters\.

 ** [name](#API_GetBot_RequestSyntax) **   <a name="lex-GetBot-request-name"></a>
The name of the bot\. The name is case sensitive\.   
Length Constraints: Minimum length of 2\. Maximum length of 50\.  
Pattern: `^([A-Za-z]_?)+$`   
Required: Yes

 ** [versionoralias](#API_GetBot_RequestSyntax) **   <a name="lex-GetBot-request-versionOrAlias"></a>
The version or alias of the bot\.  
Required: Yes

## Request Body<a name="API_GetBot_RequestBody"></a>

The request does not have a request body\.

## Response Syntax<a name="API_GetBot_ResponseSyntax"></a>

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
   "version": "string",
   "voiceId": "string"
}
```

## Response Elements<a name="API_GetBot_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [abortStatement](#API_GetBot_ResponseSyntax) **   <a name="lex-GetBot-response-abortStatement"></a>
The message that Amazon Lex returns when the user elects to end the conversation without completing it\. For more information, see [PutBot](API_PutBot.md)\.  
Type: [Statement](API_Statement.md) object

 ** [checksum](#API_GetBot_ResponseSyntax) **   <a name="lex-GetBot-response-checksum"></a>
Checksum of the bot used to identify a specific revision of the bot's `$LATEST` version\.  
Type: String

 ** [childDirected](#API_GetBot_ResponseSyntax) **   <a name="lex-GetBot-response-childDirected"></a>
For each Amazon Lex bot created with the Amazon Lex Model Building Service, you must specify whether your use of Amazon Lex is related to a website, program, or other application that is directed or targeted, in whole or in part, to children under age 13 and subject to the Children's Online Privacy Protection Act \(COPPA\) by specifying `true` or `false` in the `childDirected` field\. By specifying `true` in the `childDirected` field, you confirm that your use of Amazon Lex **is** related to a website, program, or other application that is directed or targeted, in whole or in part, to children under age 13 and subject to COPPA\. By specifying `false` in the `childDirected` field, you confirm that your use of Amazon Lex **is not** related to a website, program, or other application that is directed or targeted, in whole or in part, to children under age 13 and subject to COPPA\. You may not specify a default value for the `childDirected` field that does not accurately reflect whether your use of Amazon Lex is related to a website, program, or other application that is directed or targeted, in whole or in part, to children under age 13 and subject to COPPA\.  
If your use of Amazon Lex relates to a website, program, or other application that is directed in whole or in part, to children under age 13, you must obtain any required verifiable parental consent under COPPA\. For information regarding the use of Amazon Lex in connection with websites, programs, or other applications that are directed or targeted, in whole or in part, to children under age 13, see the [Amazon Lex FAQ\.](https://aws.amazon.com/lex/faqs#data-security)   
Type: Boolean

 ** [clarificationPrompt](#API_GetBot_ResponseSyntax) **   <a name="lex-GetBot-response-clarificationPrompt"></a>
The message Amazon Lex uses when it doesn't understand the user's request\. For more information, see [PutBot](API_PutBot.md)\.   
Type: [Prompt](API_Prompt.md) object

 ** [createdDate](#API_GetBot_ResponseSyntax) **   <a name="lex-GetBot-response-createdDate"></a>
The date that the bot was created\.  
Type: Timestamp

 ** [description](#API_GetBot_ResponseSyntax) **   <a name="lex-GetBot-response-description"></a>
A description of the bot\.  
Type: String  
Length Constraints: Minimum length of 0\. Maximum length of 200\.

 ** [detectSentiment](#API_GetBot_ResponseSyntax) **   <a name="lex-GetBot-response-detectSentiment"></a>
Indicates whether user utterances should be sent to Amazon Comprehend for sentiment analysis\.  
Type: Boolean

 ** [enableModelImprovements](#API_GetBot_ResponseSyntax) **   <a name="lex-GetBot-response-enableModelImprovements"></a>
Indicates whether the bot uses the new natural language understanding \(NLU\) model or the original NLU\. True indicates that the bot is using the new model, otherwise, false\.  
Type: Boolean

 ** [failureReason](#API_GetBot_ResponseSyntax) **   <a name="lex-GetBot-response-failureReason"></a>
If `status` is `FAILED`, Amazon Lex explains why it failed to build the bot\.  
Type: String

 ** [idleSessionTTLInSeconds](#API_GetBot_ResponseSyntax) **   <a name="lex-GetBot-response-idleSessionTTLInSeconds"></a>
The maximum time in seconds that Amazon Lex retains the data gathered in a conversation\. For more information, see [PutBot](API_PutBot.md)\.  
Type: Integer  
Valid Range: Minimum value of 60\. Maximum value of 86400\.

 ** [intents](#API_GetBot_ResponseSyntax) **   <a name="lex-GetBot-response-intents"></a>
An array of `intent` objects\. For more information, see [PutBot](API_PutBot.md)\.  
Type: Array of [Intent](API_Intent.md) objects

 ** [lastUpdatedDate](#API_GetBot_ResponseSyntax) **   <a name="lex-GetBot-response-lastUpdatedDate"></a>
The date that the bot was updated\. When you create a resource, the creation date and last updated date are the same\.   
Type: Timestamp

 ** [locale](#API_GetBot_ResponseSyntax) **   <a name="lex-GetBot-response-locale"></a>
 The target locale for the bot\.   
Type: String  
Valid Values:` en-US | en-GB | de-DE` 

 ** [name](#API_GetBot_ResponseSyntax) **   <a name="lex-GetBot-response-name"></a>
The name of the bot\.  
Type: String  
Length Constraints: Minimum length of 2\. Maximum length of 50\.  
Pattern: `^([A-Za-z]_?)+$` 

 ** [nluIntentConfidenceThreshold](#API_GetBot_ResponseSyntax) **   <a name="lex-GetBot-response-nluIntentConfidenceThreshold"></a>
The score that determines where Amazon Lex inserts the `AMAZON.FallbackIntent`, `AMAZON.KendraSearchIntent`, or both when returning alternative intents in a [PostContent](https://docs.aws.amazon.com/lex/latest/dg/API_runtime_PostContent.html) or [PostText](https://docs.aws.amazon.com/lex/latest/dg/API_runtime_PostText.html) response\. `AMAZON.FallbackIntent` is inserted if the confidence score for all intents is below this value\. `AMAZON.KendraSearchIntent` is only inserted if it is configured for the bot\.  
Type: Double  
Valid Range: Minimum value of 0\. Maximum value of 1\.

 ** [status](#API_GetBot_ResponseSyntax) **   <a name="lex-GetBot-response-status"></a>
The status of the bot\.   
When the status is `BUILDING` Amazon Lex is building the bot for testing and use\.  
If the status of the bot is `READY_BASIC_TESTING`, you can test the bot using the exact utterances specified in the bot's intents\. When the bot is ready for full testing or to run, the status is `READY`\.  
If there was a problem with building the bot, the status is `FAILED` and the `failureReason` field explains why the bot did not build\.  
If the bot was saved but not built, the status is `NOT_BUILT`\.  
Type: String  
Valid Values:` BUILDING | READY | READY_BASIC_TESTING | FAILED | NOT_BUILT` 

 ** [version](#API_GetBot_ResponseSyntax) **   <a name="lex-GetBot-response-version"></a>
The version of the bot\. For a new bot, the version is always `$LATEST`\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 64\.  
Pattern: `\$LATEST|[0-9]+` 

 ** [voiceId](#API_GetBot_ResponseSyntax) **   <a name="lex-GetBot-response-voiceId"></a>
The Amazon Polly voice ID that Amazon Lex uses for voice interaction with the user\. For more information, see [PutBot](API_PutBot.md)\.  
Type: String

## Errors<a name="API_GetBot_Errors"></a>

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

## See Also<a name="API_GetBot_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/lex-models-2017-04-19/GetBot) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/lex-models-2017-04-19/GetBot) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/lex-models-2017-04-19/GetBot) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/lex-models-2017-04-19/GetBot) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/lex-models-2017-04-19/GetBot) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/lex-models-2017-04-19/GetBot) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/lex-models-2017-04-19/GetBot) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/lex-models-2017-04-19/GetBot) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/lex-models-2017-04-19/GetBot) 