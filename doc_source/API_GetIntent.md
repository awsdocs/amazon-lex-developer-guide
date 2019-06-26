# GetIntent<a name="API_GetIntent"></a>

 Returns information about an intent\. In addition to the intent name, you must specify the intent version\. 

 This operation requires permissions to perform the `lex:GetIntent` action\. 

## Request Syntax<a name="API_GetIntent_RequestSyntax"></a>

```
GET /intents/name/versions/version HTTP/1.1
```

## URI Request Parameters<a name="API_GetIntent_RequestParameters"></a>

The request requires the following URI parameters\.

 ** [name](#API_GetIntent_RequestSyntax) **   <a name="lex-GetIntent-request-name"></a>
The name of the intent\. The name is case sensitive\.   
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `^([A-Za-z]_?)+$` 

 ** [version](#API_GetIntent_RequestSyntax) **   <a name="lex-GetIntent-request-version"></a>
The version of the intent\.  
Length Constraints: Minimum length of 1\. Maximum length of 64\.  
Pattern: `\$LATEST|[0-9]+` 

## Request Body<a name="API_GetIntent_RequestBody"></a>

The request does not have a request body\.

## Response Syntax<a name="API_GetIntent_ResponseSyntax"></a>

```
HTTP/1.1 200
Content-type: application/json

{
   "[checksum](#lex-GetIntent-response-checksum)": "string",
   "[conclusionStatement](#lex-GetIntent-response-conclusionStatement)": { 
      "[messages](API_Statement.md#lex-Type-Statement-messages)": [ 
         { 
            "[content](API_Message.md#lex-Type-Message-content)": "string",
            "[contentType](API_Message.md#lex-Type-Message-contentType)": "string",
            "[groupNumber](API_Message.md#lex-Type-Message-groupNumber)": number
         }
      ],
      "[responseCard](API_Statement.md#lex-Type-Statement-responseCard)": "string"
   },
   "[confirmationPrompt](#lex-GetIntent-response-confirmationPrompt)": { 
      "[maxAttempts](API_Prompt.md#lex-Type-Prompt-maxAttempts)": number,
      "[messages](API_Prompt.md#lex-Type-Prompt-messages)": [ 
         { 
            "[content](API_Message.md#lex-Type-Message-content)": "string",
            "[contentType](API_Message.md#lex-Type-Message-contentType)": "string",
            "[groupNumber](API_Message.md#lex-Type-Message-groupNumber)": number
         }
      ],
      "[responseCard](API_Prompt.md#lex-Type-Prompt-responseCard)": "string"
   },
   "[createdDate](#lex-GetIntent-response-createdDate)": number,
   "[description](#lex-GetIntent-response-description)": "string",
   "[dialogCodeHook](#lex-GetIntent-response-dialogCodeHook)": { 
      "[messageVersion](API_CodeHook.md#lex-Type-CodeHook-messageVersion)": "string",
      "[uri](API_CodeHook.md#lex-Type-CodeHook-uri)": "string"
   },
   "[followUpPrompt](#lex-GetIntent-response-followUpPrompt)": { 
      "[prompt](API_FollowUpPrompt.md#lex-Type-FollowUpPrompt-prompt)": { 
         "[maxAttempts](API_Prompt.md#lex-Type-Prompt-maxAttempts)": number,
         "[messages](API_Prompt.md#lex-Type-Prompt-messages)": [ 
            { 
               "[content](API_Message.md#lex-Type-Message-content)": "string",
               "[contentType](API_Message.md#lex-Type-Message-contentType)": "string",
               "[groupNumber](API_Message.md#lex-Type-Message-groupNumber)": number
            }
         ],
         "[responseCard](API_Prompt.md#lex-Type-Prompt-responseCard)": "string"
      },
      "[rejectionStatement](API_FollowUpPrompt.md#lex-Type-FollowUpPrompt-rejectionStatement)": { 
         "[messages](API_Statement.md#lex-Type-Statement-messages)": [ 
            { 
               "[content](API_Message.md#lex-Type-Message-content)": "string",
               "[contentType](API_Message.md#lex-Type-Message-contentType)": "string",
               "[groupNumber](API_Message.md#lex-Type-Message-groupNumber)": number
            }
         ],
         "[responseCard](API_Statement.md#lex-Type-Statement-responseCard)": "string"
      }
   },
   "[fulfillmentActivity](#lex-GetIntent-response-fulfillmentActivity)": { 
      "[codeHook](API_FulfillmentActivity.md#lex-Type-FulfillmentActivity-codeHook)": { 
         "[messageVersion](API_CodeHook.md#lex-Type-CodeHook-messageVersion)": "string",
         "[uri](API_CodeHook.md#lex-Type-CodeHook-uri)": "string"
      },
      "[type](API_FulfillmentActivity.md#lex-Type-FulfillmentActivity-type)": "string"
   },
   "[lastUpdatedDate](#lex-GetIntent-response-lastUpdatedDate)": number,
   "[name](#lex-GetIntent-response-name)": "string",
   "[parentIntentSignature](#lex-GetIntent-response-parentIntentSignature)": "string",
   "[rejectionStatement](#lex-GetIntent-response-rejectionStatement)": { 
      "[messages](API_Statement.md#lex-Type-Statement-messages)": [ 
         { 
            "[content](API_Message.md#lex-Type-Message-content)": "string",
            "[contentType](API_Message.md#lex-Type-Message-contentType)": "string",
            "[groupNumber](API_Message.md#lex-Type-Message-groupNumber)": number
         }
      ],
      "[responseCard](API_Statement.md#lex-Type-Statement-responseCard)": "string"
   },
   "[sampleUtterances](#lex-GetIntent-response-sampleUtterances)": [ "string" ],
   "[slots](#lex-GetIntent-response-slots)": [ 
      { 
         "[description](API_Slot.md#lex-Type-Slot-description)": "string",
         "[name](API_Slot.md#lex-Type-Slot-name)": "string",
         "[priority](API_Slot.md#lex-Type-Slot-priority)": number,
         "[responseCard](API_Slot.md#lex-Type-Slot-responseCard)": "string",
         "[sampleUtterances](API_Slot.md#lex-Type-Slot-sampleUtterances)": [ "string" ],
         "[slotConstraint](API_Slot.md#lex-Type-Slot-slotConstraint)": "string",
         "[slotType](API_Slot.md#lex-Type-Slot-slotType)": "string",
         "[slotTypeVersion](API_Slot.md#lex-Type-Slot-slotTypeVersion)": "string",
         "[valueElicitationPrompt](API_Slot.md#lex-Type-Slot-valueElicitationPrompt)": { 
            "[maxAttempts](API_Prompt.md#lex-Type-Prompt-maxAttempts)": number,
            "[messages](API_Prompt.md#lex-Type-Prompt-messages)": [ 
               { 
                  "[content](API_Message.md#lex-Type-Message-content)": "string",
                  "[contentType](API_Message.md#lex-Type-Message-contentType)": "string",
                  "[groupNumber](API_Message.md#lex-Type-Message-groupNumber)": number
               }
            ],
            "[responseCard](API_Prompt.md#lex-Type-Prompt-responseCard)": "string"
         }
      }
   ],
   "[version](#lex-GetIntent-response-version)": "string"
}
```

## Response Elements<a name="API_GetIntent_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [checksum](#API_GetIntent_ResponseSyntax) **   <a name="lex-GetIntent-response-checksum"></a>
Checksum of the intent\.  
Type: String

 ** [conclusionStatement](#API_GetIntent_ResponseSyntax) **   <a name="lex-GetIntent-response-conclusionStatement"></a>
After the Lambda function specified in the `fulfillmentActivity` element fulfills the intent, Amazon Lex conveys this statement to the user\.  
Type: [Statement](API_Statement.md) object

 ** [confirmationPrompt](#API_GetIntent_ResponseSyntax) **   <a name="lex-GetIntent-response-confirmationPrompt"></a>
If defined in the bot, Amazon Lex uses prompt to confirm the intent before fulfilling the user's request\. For more information, see [PutIntent](API_PutIntent.md)\.   
Type: [Prompt](API_Prompt.md) object

 ** [createdDate](#API_GetIntent_ResponseSyntax) **   <a name="lex-GetIntent-response-createdDate"></a>
The date that the intent was created\.  
Type: Timestamp

 ** [description](#API_GetIntent_ResponseSyntax) **   <a name="lex-GetIntent-response-description"></a>
A description of the intent\.  
Type: String  
Length Constraints: Minimum length of 0\. Maximum length of 200\.

 ** [dialogCodeHook](#API_GetIntent_ResponseSyntax) **   <a name="lex-GetIntent-response-dialogCodeHook"></a>
If defined in the bot, Amazon Amazon Lex invokes this Lambda function for each user input\. For more information, see [PutIntent](API_PutIntent.md)\.   
Type: [CodeHook](API_CodeHook.md) object

 ** [followUpPrompt](#API_GetIntent_ResponseSyntax) **   <a name="lex-GetIntent-response-followUpPrompt"></a>
If defined in the bot, Amazon Lex uses this prompt to solicit additional user activity after the intent is fulfilled\. For more information, see [PutIntent](API_PutIntent.md)\.  
Type: [FollowUpPrompt](API_FollowUpPrompt.md) object

 ** [fulfillmentActivity](#API_GetIntent_ResponseSyntax) **   <a name="lex-GetIntent-response-fulfillmentActivity"></a>
Describes how the intent is fulfilled\. For more information, see [PutIntent](API_PutIntent.md)\.   
Type: [FulfillmentActivity](API_FulfillmentActivity.md) object

 ** [lastUpdatedDate](#API_GetIntent_ResponseSyntax) **   <a name="lex-GetIntent-response-lastUpdatedDate"></a>
The date that the intent was updated\. When you create a resource, the creation date and the last updated date are the same\.   
Type: Timestamp

 ** [name](#API_GetIntent_ResponseSyntax) **   <a name="lex-GetIntent-response-name"></a>
The name of the intent\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `^([A-Za-z]_?)+$` 

 ** [parentIntentSignature](#API_GetIntent_ResponseSyntax) **   <a name="lex-GetIntent-response-parentIntentSignature"></a>
A unique identifier for a built\-in intent\.  
Type: String

 ** [rejectionStatement](#API_GetIntent_ResponseSyntax) **   <a name="lex-GetIntent-response-rejectionStatement"></a>
If the user answers "no" to the question defined in `confirmationPrompt`, Amazon Lex responds with this statement to acknowledge that the intent was canceled\.   
Type: [Statement](API_Statement.md) object

 ** [sampleUtterances](#API_GetIntent_ResponseSyntax) **   <a name="lex-GetIntent-response-sampleUtterances"></a>
An array of sample utterances configured for the intent\.  
Type: Array of strings  
Array Members: Minimum number of 0 items\. Maximum number of 1500 items\.  
Length Constraints: Minimum length of 1\. Maximum length of 200\.

 ** [slots](#API_GetIntent_ResponseSyntax) **   <a name="lex-GetIntent-response-slots"></a>
An array of intent slots configured for the intent\.  
Type: Array of [Slot](API_Slot.md) objects  
Array Members: Minimum number of 0 items\. Maximum number of 100 items\.

 ** [version](#API_GetIntent_ResponseSyntax) **   <a name="lex-GetIntent-response-version"></a>
The version of the intent\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 64\.  
Pattern: `\$LATEST|[0-9]+` 

## Errors<a name="API_GetIntent_Errors"></a>

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

## See Also<a name="API_GetIntent_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/lex-models-2017-04-19/GetIntent) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/lex-models-2017-04-19/GetIntent) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/lex-models-2017-04-19/GetIntent) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/lex-models-2017-04-19/GetIntent) 
+  [AWS SDK for Go \- Pilot](https://docs.aws.amazon.com/goto/SdkForGoPilot/lex-models-2017-04-19/GetIntent) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/lex-models-2017-04-19/GetIntent) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/lex-models-2017-04-19/GetIntent) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/lex-models-2017-04-19/GetIntent) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/lex-models-2017-04-19/GetIntent) 
+  [AWS SDK for Ruby V2](https://docs.aws.amazon.com/goto/SdkForRubyV2/lex-models-2017-04-19/GetIntent) 