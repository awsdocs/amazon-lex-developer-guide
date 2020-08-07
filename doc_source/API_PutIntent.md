# PutIntent<a name="API_PutIntent"></a>

Creates an intent or replaces an existing intent\.

To define the interaction between the user and your bot, you use one or more intents\. For a pizza ordering bot, for example, you would create an `OrderPizza` intent\. 

To create an intent or replace an existing intent, you must provide the following:
+ Intent name\. For example, `OrderPizza`\.
+ Sample utterances\. For example, "Can I order a pizza, please\." and "I want to order a pizza\."
+ Information to be gathered\. You specify slot types for the information that your bot will request from the user\. You can specify standard slot types, such as a date or a time, or custom slot types such as the size and crust of a pizza\.
+ How the intent will be fulfilled\. You can provide a Lambda function or configure the intent to return the intent information to the client application\. If you use a Lambda function, when all of the intent information is available, Amazon Lex invokes your Lambda function\. If you configure your intent to return the intent information to the client application\. 

You can specify other optional information in the request, such as:
+ A confirmation prompt to ask the user to confirm an intent\. For example, "Shall I order your pizza?"
+ A conclusion statement to send to the user after the intent has been fulfilled\. For example, "I placed your pizza order\."
+ A follow\-up prompt that asks the user for additional activity\. For example, asking "Do you want to order a drink with your pizza?"

If you specify an existing intent name to update the intent, Amazon Lex replaces the values in the `$LATEST` version of the intent with the values in the request\. Amazon Lex removes fields that you don't provide in the request\. If you don't specify the required fields, Amazon Lex throws an exception\. When you update the `$LATEST` version of an intent, the `status` field of any bot that uses the `$LATEST` version of the intent is set to `NOT_BUILT`\.

For more information, see [Amazon Lex: How It Works](how-it-works.md)\.

This operation requires permissions for the `lex:PutIntent` action\.

## Request Syntax<a name="API_PutIntent_RequestSyntax"></a>

```
PUT /intents/name/versions/$LATEST HTTP/1.1
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
   "createVersion": boolean,
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
   ]
}
```

## URI Request Parameters<a name="API_PutIntent_RequestParameters"></a>

The request uses the following URI parameters\.

 ** [name](#API_PutIntent_RequestSyntax) **   <a name="lex-PutIntent-request-name"></a>
The name of the intent\. The name is *not* case sensitive\.   
The name can't match a built\-in intent name, or a built\-in intent name with "AMAZON\." removed\. For example, because there is a built\-in intent called `AMAZON.HelpIntent`, you can't create a custom intent called `HelpIntent`\.  
For a list of built\-in intents, see [Standard Built\-in Intents](https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit/docs/built-in-intent-ref/standard-intents) in the *Alexa Skills Kit*\.  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `^([A-Za-z]_?)+$`   
Required: Yes

## Request Body<a name="API_PutIntent_RequestBody"></a>

The request accepts the following data in JSON format\.

 ** [checksum](#API_PutIntent_RequestSyntax) **   <a name="lex-PutIntent-request-checksum"></a>
Identifies a specific revision of the `$LATEST` version\.  
When you create a new intent, leave the `checksum` field blank\. If you specify a checksum you get a `BadRequestException` exception\.  
When you want to update a intent, set the `checksum` field to the checksum of the most recent revision of the `$LATEST` version\. If you don't specify the ` checksum` field, or if the checksum does not match the `$LATEST` version, you get a `PreconditionFailedException` exception\.  
Type: String  
Required: No

 ** [conclusionStatement](#API_PutIntent_RequestSyntax) **   <a name="lex-PutIntent-request-conclusionStatement"></a>
 The statement that you want Amazon Lex to convey to the user after the intent is successfully fulfilled by the Lambda function\.   
This element is relevant only if you provide a Lambda function in the `fulfillmentActivity`\. If you return the intent to the client application, you can't specify this element\.  
The `followUpPrompt` and `conclusionStatement` are mutually exclusive\. You can specify only one\.
Type: [Statement](API_Statement.md) object  
Required: No

 ** [confirmationPrompt](#API_PutIntent_RequestSyntax) **   <a name="lex-PutIntent-request-confirmationPrompt"></a>
Prompts the user to confirm the intent\. This question should have a yes or no answer\.  
Amazon Lex uses this prompt to ensure that the user acknowledges that the intent is ready for fulfillment\. For example, with the `OrderPizza` intent, you might want to confirm that the order is correct before placing it\. For other intents, such as intents that simply respond to user questions, you might not need to ask the user for confirmation before providing the information\.   
You you must provide both the `rejectionStatement` and the `confirmationPrompt`, or neither\.
Type: [Prompt](API_Prompt.md) object  
Required: No

 ** [createVersion](#API_PutIntent_RequestSyntax) **   <a name="lex-PutIntent-request-createVersion"></a>
When set to `true` a new numbered version of the intent is created\. This is the same as calling the `CreateIntentVersion` operation\. If you do not specify `createVersion`, the default is `false`\.  
Type: Boolean  
Required: No

 ** [description](#API_PutIntent_RequestSyntax) **   <a name="lex-PutIntent-request-description"></a>
A description of the intent\.  
Type: String  
Length Constraints: Minimum length of 0\. Maximum length of 200\.  
Required: No

 ** [dialogCodeHook](#API_PutIntent_RequestSyntax) **   <a name="lex-PutIntent-request-dialogCodeHook"></a>
 Specifies a Lambda function to invoke for each user input\. You can invoke this Lambda function to personalize user interaction\.   
For example, suppose your bot determines that the user is John\. Your Lambda function might retrieve John's information from a backend database and prepopulate some of the values\. For example, if you find that John is gluten intolerant, you might set the corresponding intent slot, `GlutenIntolerant`, to true\. You might find John's phone number and set the corresponding session attribute\.   
Type: [CodeHook](API_CodeHook.md) object  
Required: No

 ** [followUpPrompt](#API_PutIntent_RequestSyntax) **   <a name="lex-PutIntent-request-followUpPrompt"></a>
Amazon Lex uses this prompt to solicit additional activity after fulfilling an intent\. For example, after the `OrderPizza` intent is fulfilled, you might prompt the user to order a drink\.  
The action that Amazon Lex takes depends on the user's response, as follows:  
+ If the user says "Yes" it responds with the clarification prompt that is configured for the bot\.
+ if the user says "Yes" and continues with an utterance that triggers an intent it starts a conversation for the intent\.
+ If the user says "No" it responds with the rejection statement configured for the the follow\-up prompt\.
+ If it doesn't recognize the utterance it repeats the follow\-up prompt again\.
The `followUpPrompt` field and the `conclusionStatement` field are mutually exclusive\. You can specify only one\.   
Type: [FollowUpPrompt](API_FollowUpPrompt.md) object  
Required: No

 ** [fulfillmentActivity](#API_PutIntent_RequestSyntax) **   <a name="lex-PutIntent-request-fulfillmentActivity"></a>
Required\. Describes how the intent is fulfilled\. For example, after a user provides all of the information for a pizza order, `fulfillmentActivity` defines how the bot places an order with a local pizza store\.   
 You might configure Amazon Lex to return all of the intent information to the client application, or direct it to invoke a Lambda function that can process the intent \(for example, place an order with a pizzeria\)\.   
Type: [FulfillmentActivity](API_FulfillmentActivity.md) object  
Required: No

 ** [kendraConfiguration](#API_PutIntent_RequestSyntax) **   <a name="lex-PutIntent-request-kendraConfiguration"></a>
Configuration information required to use the `AMAZON.KendraSearchIntent` intent to connect to an Amazon Kendra index\. For more information, see [ AMAZON\.KendraSearchIntent](http://docs.aws.amazon.com/lex/latest/dg/built-in-intent-kendra-search.html)\.  
Type: [KendraConfiguration](API_KendraConfiguration.md) object  
Required: No

 ** [parentIntentSignature](#API_PutIntent_RequestSyntax) **   <a name="lex-PutIntent-request-parentIntentSignature"></a>
A unique identifier for the built\-in intent to base this intent on\. To find the signature for an intent, see [Standard Built\-in Intents](https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit/docs/built-in-intent-ref/standard-intents) in the *Alexa Skills Kit*\.  
Type: String  
Required: No

 ** [rejectionStatement](#API_PutIntent_RequestSyntax) **   <a name="lex-PutIntent-request-rejectionStatement"></a>
When the user answers "no" to the question defined in `confirmationPrompt`, Amazon Lex responds with this statement to acknowledge that the intent was canceled\.   
You must provide both the `rejectionStatement` and the `confirmationPrompt`, or neither\.
Type: [Statement](API_Statement.md) object  
Required: No

 ** [sampleUtterances](#API_PutIntent_RequestSyntax) **   <a name="lex-PutIntent-request-sampleUtterances"></a>
An array of utterances \(strings\) that a user might say to signal the intent\. For example, "I want \{PizzaSize\} pizza", "Order \{Quantity\} \{PizzaSize\} pizzas"\.   
In each utterance, a slot name is enclosed in curly braces\.   
Type: Array of strings  
Array Members: Minimum number of 0 items\. Maximum number of 1500 items\.  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Required: No

 ** [slots](#API_PutIntent_RequestSyntax) **   <a name="lex-PutIntent-request-slots"></a>
An array of intent slots\. At runtime, Amazon Lex elicits required slot values from the user using prompts defined in the slots\. For more information, see [Amazon Lex: How It Works](how-it-works.md)\.   
Type: Array of [Slot](API_Slot.md) objects  
Array Members: Minimum number of 0 items\. Maximum number of 100 items\.  
Required: No

## Response Syntax<a name="API_PutIntent_ResponseSyntax"></a>

```
HTTP/1.1 200
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
   "createVersion": boolean,
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

## Response Elements<a name="API_PutIntent_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [checksum](#API_PutIntent_ResponseSyntax) **   <a name="lex-PutIntent-response-checksum"></a>
Checksum of the `$LATEST`version of the intent created or updated\.  
Type: String

 ** [conclusionStatement](#API_PutIntent_ResponseSyntax) **   <a name="lex-PutIntent-response-conclusionStatement"></a>
After the Lambda function specified in the`fulfillmentActivity`intent fulfills the intent, Amazon Lex conveys this statement to the user\.  
Type: [Statement](API_Statement.md) object

 ** [confirmationPrompt](#API_PutIntent_ResponseSyntax) **   <a name="lex-PutIntent-response-confirmationPrompt"></a>
If defined in the intent, Amazon Lex prompts the user to confirm the intent before fulfilling it\.  
Type: [Prompt](API_Prompt.md) object

 ** [createdDate](#API_PutIntent_ResponseSyntax) **   <a name="lex-PutIntent-response-createdDate"></a>
The date that the intent was created\.  
Type: Timestamp

 ** [createVersion](#API_PutIntent_ResponseSyntax) **   <a name="lex-PutIntent-response-createVersion"></a>
 `True` if a new version of the intent was created\. If the `createVersion` field was not specified in the request, the `createVersion` field is set to false in the response\.  
Type: Boolean

 ** [description](#API_PutIntent_ResponseSyntax) **   <a name="lex-PutIntent-response-description"></a>
A description of the intent\.  
Type: String  
Length Constraints: Minimum length of 0\. Maximum length of 200\.

 ** [dialogCodeHook](#API_PutIntent_ResponseSyntax) **   <a name="lex-PutIntent-response-dialogCodeHook"></a>
If defined in the intent, Amazon Lex invokes this Lambda function for each user input\.  
Type: [CodeHook](API_CodeHook.md) object

 ** [followUpPrompt](#API_PutIntent_ResponseSyntax) **   <a name="lex-PutIntent-response-followUpPrompt"></a>
If defined in the intent, Amazon Lex uses this prompt to solicit additional user activity after the intent is fulfilled\.  
Type: [FollowUpPrompt](API_FollowUpPrompt.md) object

 ** [fulfillmentActivity](#API_PutIntent_ResponseSyntax) **   <a name="lex-PutIntent-response-fulfillmentActivity"></a>
If defined in the intent, Amazon Lex invokes this Lambda function to fulfill the intent after the user provides all of the information required by the intent\.  
Type: [FulfillmentActivity](API_FulfillmentActivity.md) object

 ** [kendraConfiguration](#API_PutIntent_ResponseSyntax) **   <a name="lex-PutIntent-response-kendraConfiguration"></a>
Configuration information, if any, required to connect to an Amazon Kendra index and use the `AMAZON.KendraSearchIntent` intent\.  
Type: [KendraConfiguration](API_KendraConfiguration.md) object

 ** [lastUpdatedDate](#API_PutIntent_ResponseSyntax) **   <a name="lex-PutIntent-response-lastUpdatedDate"></a>
The date that the intent was updated\. When you create a resource, the creation date and last update dates are the same\.  
Type: Timestamp

 ** [name](#API_PutIntent_ResponseSyntax) **   <a name="lex-PutIntent-response-name"></a>
The name of the intent\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `^([A-Za-z]_?)+$` 

 ** [parentIntentSignature](#API_PutIntent_ResponseSyntax) **   <a name="lex-PutIntent-response-parentIntentSignature"></a>
A unique identifier for the built\-in intent that this intent is based on\.  
Type: String

 ** [rejectionStatement](#API_PutIntent_ResponseSyntax) **   <a name="lex-PutIntent-response-rejectionStatement"></a>
If the user answers "no" to the question defined in `confirmationPrompt` Amazon Lex responds with this statement to acknowledge that the intent was canceled\.   
Type: [Statement](API_Statement.md) object

 ** [sampleUtterances](#API_PutIntent_ResponseSyntax) **   <a name="lex-PutIntent-response-sampleUtterances"></a>
 An array of sample utterances that are configured for the intent\.   
Type: Array of strings  
Array Members: Minimum number of 0 items\. Maximum number of 1500 items\.  
Length Constraints: Minimum length of 1\. Maximum length of 200\.

 ** [slots](#API_PutIntent_ResponseSyntax) **   <a name="lex-PutIntent-response-slots"></a>
An array of intent slots that are configured for the intent\.  
Type: Array of [Slot](API_Slot.md) objects  
Array Members: Minimum number of 0 items\. Maximum number of 100 items\.

 ** [version](#API_PutIntent_ResponseSyntax) **   <a name="lex-PutIntent-response-version"></a>
The version of the intent\. For a new intent, the version is always `$LATEST`\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 64\.  
Pattern: `\$LATEST|[0-9]+` 

## Errors<a name="API_PutIntent_Errors"></a>

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

## See Also<a name="API_PutIntent_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/lex-models-2017-04-19/PutIntent) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/lex-models-2017-04-19/PutIntent) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/lex-models-2017-04-19/PutIntent) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/lex-models-2017-04-19/PutIntent) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/lex-models-2017-04-19/PutIntent) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/lex-models-2017-04-19/PutIntent) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/lex-models-2017-04-19/PutIntent) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/lex-models-2017-04-19/PutIntent) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/lex-models-2017-04-19/PutIntent) 