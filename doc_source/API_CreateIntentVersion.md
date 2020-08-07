# CreateIntentVersion<a name="API_CreateIntentVersion"></a>

Creates a new version of an intent based on the `$LATEST` version of the intent\. If the `$LATEST` version of this intent hasn't changed since you last updated it, Amazon Lex doesn't create a new version\. It returns the last version you created\.

**Note**  
You can update only the `$LATEST` version of the intent\. You can't update the numbered versions that you create with the `CreateIntentVersion` operation\.

 When you create a version of an intent, Amazon Lex sets the version to 1\. Subsequent versions increment by 1\. For more information, see [Versioning](versioning-aliases.md#versioning-intro)\. 

This operation requires permissions to perform the `lex:CreateIntentVersion` action\. 

## Request Syntax<a name="API_CreateIntentVersion_RequestSyntax"></a>

```
POST /intents/name/versions HTTP/1.1
Content-type: application/json

{
   "checksum": "string"
}
```

## URI Request Parameters<a name="API_CreateIntentVersion_RequestParameters"></a>

The request uses the following URI parameters\.

 ** [name](#API_CreateIntentVersion_RequestSyntax) **   <a name="lex-CreateIntentVersion-request-name"></a>
The name of the intent that you want to create a new version of\. The name is case sensitive\.   
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `^([A-Za-z]_?)+$`   
Required: Yes

## Request Body<a name="API_CreateIntentVersion_RequestBody"></a>

The request accepts the following data in JSON format\.

 ** [checksum](#API_CreateIntentVersion_RequestSyntax) **   <a name="lex-CreateIntentVersion-request-checksum"></a>
Checksum of the `$LATEST` version of the intent that should be used to create the new version\. If you specify a checksum and the `$LATEST` version of the intent has a different checksum, Amazon Lex returns a `PreconditionFailedException` exception and doesn't publish a new version\. If you don't specify a checksum, Amazon Lex publishes the `$LATEST` version\.  
Type: String  
Required: No

## Response Syntax<a name="API_CreateIntentVersion_ResponseSyntax"></a>

```
HTTP/1.1 201
Content-type: application/json

{
   "checksum": "string",
   "conclusionStatement": { 
      "messages": [ 
         { 
            "content": "string",
            "contentType": "string",
            "groupNumber": number
         }
      ],
      "responseCard": "string"
   },
   "confirmationPrompt": { 
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
   "dialogCodeHook": { 
      "messageVersion": "string",
      "uri": "string"
   },
   "followUpPrompt": { 
      "prompt": { 
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
      "rejectionStatement": { 
         "messages": [ 
            { 
               "content": "string",
               "contentType": "string",
               "groupNumber": number
            }
         ],
         "responseCard": "string"
      }
   },
   "fulfillmentActivity": { 
      "codeHook": { 
         "messageVersion": "string",
         "uri": "string"
      },
      "type": "string"
   },
   "kendraConfiguration": { 
      "kendraIndex": "string",
      "queryFilterString": "string",
      "role": "string"
   },
   "lastUpdatedDate": number,
   "name": "string",
   "parentIntentSignature": "string",
   "rejectionStatement": { 
      "messages": [ 
         { 
            "content": "string",
            "contentType": "string",
            "groupNumber": number
         }
      ],
      "responseCard": "string"
   },
   "sampleUtterances": [ "string" ],
   "slots": [ 
      { 
         "description": "string",
         "name": "string",
         "obfuscationSetting": "string",
         "priority": number,
         "responseCard": "string",
         "sampleUtterances": [ "string" ],
         "slotConstraint": "string",
         "slotType": "string",
         "slotTypeVersion": "string",
         "valueElicitationPrompt": { 
            "maxAttempts": number,
            "messages": [ 
               { 
                  "content": "string",
                  "contentType": "string",
                  "groupNumber": number
               }
            ],
            "responseCard": "string"
         }
      }
   ],
   "version": "string"
}
```

## Response Elements<a name="API_CreateIntentVersion_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 201 response\.

The following data is returned in JSON format by the service\.

 ** [checksum](#API_CreateIntentVersion_ResponseSyntax) **   <a name="lex-CreateIntentVersion-response-checksum"></a>
Checksum of the intent version created\.  
Type: String

 ** [conclusionStatement](#API_CreateIntentVersion_ResponseSyntax) **   <a name="lex-CreateIntentVersion-response-conclusionStatement"></a>
After the Lambda function specified in the `fulfillmentActivity` field fulfills the intent, Amazon Lex conveys this statement to the user\.   
Type: [Statement](API_Statement.md) object

 ** [confirmationPrompt](#API_CreateIntentVersion_ResponseSyntax) **   <a name="lex-CreateIntentVersion-response-confirmationPrompt"></a>
If defined, the prompt that Amazon Lex uses to confirm the user's intent before fulfilling it\.   
Type: [Prompt](API_Prompt.md) object

 ** [createdDate](#API_CreateIntentVersion_ResponseSyntax) **   <a name="lex-CreateIntentVersion-response-createdDate"></a>
The date that the intent was created\.  
Type: Timestamp

 ** [description](#API_CreateIntentVersion_ResponseSyntax) **   <a name="lex-CreateIntentVersion-response-description"></a>
A description of the intent\.  
Type: String  
Length Constraints: Minimum length of 0\. Maximum length of 200\.

 ** [dialogCodeHook](#API_CreateIntentVersion_ResponseSyntax) **   <a name="lex-CreateIntentVersion-response-dialogCodeHook"></a>
If defined, Amazon Lex invokes this Lambda function for each user input\.  
Type: [CodeHook](API_CodeHook.md) object

 ** [followUpPrompt](#API_CreateIntentVersion_ResponseSyntax) **   <a name="lex-CreateIntentVersion-response-followUpPrompt"></a>
If defined, Amazon Lex uses this prompt to solicit additional user activity after the intent is fulfilled\.   
Type: [FollowUpPrompt](API_FollowUpPrompt.md) object

 ** [fulfillmentActivity](#API_CreateIntentVersion_ResponseSyntax) **   <a name="lex-CreateIntentVersion-response-fulfillmentActivity"></a>
 Describes how the intent is fulfilled\.   
Type: [FulfillmentActivity](API_FulfillmentActivity.md) object

 ** [kendraConfiguration](#API_CreateIntentVersion_ResponseSyntax) **   <a name="lex-CreateIntentVersion-response-kendraConfiguration"></a>
Configuration information, if any, for connectin an Amazon Kendra index with the `AMAZON.KendraSearchIntent` intent\.  
Type: [KendraConfiguration](API_KendraConfiguration.md) object

 ** [lastUpdatedDate](#API_CreateIntentVersion_ResponseSyntax) **   <a name="lex-CreateIntentVersion-response-lastUpdatedDate"></a>
The date that the intent was updated\.   
Type: Timestamp

 ** [name](#API_CreateIntentVersion_ResponseSyntax) **   <a name="lex-CreateIntentVersion-response-name"></a>
The name of the intent\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `^([A-Za-z]_?)+$` 

 ** [parentIntentSignature](#API_CreateIntentVersion_ResponseSyntax) **   <a name="lex-CreateIntentVersion-response-parentIntentSignature"></a>
A unique identifier for a built\-in intent\.  
Type: String

 ** [rejectionStatement](#API_CreateIntentVersion_ResponseSyntax) **   <a name="lex-CreateIntentVersion-response-rejectionStatement"></a>
If the user answers "no" to the question defined in `confirmationPrompt`, Amazon Lex responds with this statement to acknowledge that the intent was canceled\.   
Type: [Statement](API_Statement.md) object

 ** [sampleUtterances](#API_CreateIntentVersion_ResponseSyntax) **   <a name="lex-CreateIntentVersion-response-sampleUtterances"></a>
An array of sample utterances configured for the intent\.   
Type: Array of strings  
Array Members: Minimum number of 0 items\. Maximum number of 1500 items\.  
Length Constraints: Minimum length of 1\. Maximum length of 200\.

 ** [slots](#API_CreateIntentVersion_ResponseSyntax) **   <a name="lex-CreateIntentVersion-response-slots"></a>
An array of slot types that defines the information required to fulfill the intent\.  
Type: Array of [Slot](API_Slot.md) objects  
Array Members: Minimum number of 0 items\. Maximum number of 100 items\.

 ** [version](#API_CreateIntentVersion_ResponseSyntax) **   <a name="lex-CreateIntentVersion-response-version"></a>
The version number assigned to the new version of the intent\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 64\.  
Pattern: `\$LATEST|[0-9]+` 

## Errors<a name="API_CreateIntentVersion_Errors"></a>

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

 **NotFoundException**   
The resource specified in the request was not found\. Check the resource and try again\.  
HTTP Status Code: 404

 **PreconditionFailedException**   
 The checksum of the resource that you are trying to change does not match the checksum in the request\. Check the resource's checksum and try again\.  
HTTP Status Code: 412

## See Also<a name="API_CreateIntentVersion_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/lex-models-2017-04-19/CreateIntentVersion) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/lex-models-2017-04-19/CreateIntentVersion) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/lex-models-2017-04-19/CreateIntentVersion) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/lex-models-2017-04-19/CreateIntentVersion) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/lex-models-2017-04-19/CreateIntentVersion) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/lex-models-2017-04-19/CreateIntentVersion) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/lex-models-2017-04-19/CreateIntentVersion) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/lex-models-2017-04-19/CreateIntentVersion) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/lex-models-2017-04-19/CreateIntentVersion) 