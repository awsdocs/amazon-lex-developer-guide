# Lambda Function Input Event and Response Format<a name="lambda-input-response-format"></a>

This section describes the structure of the event data that Amazon Lex provides to a Lambda function\. Use this information to parse the input in your Lambda code\. It also explains the format of the response that Amazon Lex expects your Lambda function to return\. 

**Topics**
+ [Input Event Format](#using-lambda-input-event-format)
+ [Response Format](#using-lambda-response-format)

## Input Event Format<a name="using-lambda-input-event-format"></a>

The following shows the general format of an Amazon Lex event that is passed to a Lambda function\. Use this information when you are writing your Lambda function\.

**Note**  
The input format may change without a corresponding change in the `messageVersion`\. Your code should not throw an error if new fields are present\.

```
{
  "currentIntent": {
    "name": "intent-name",
    "nluIntentConfidenceScore": score,
    "slots": {
      "slot name": "value",
      "slot name": "value"
    },
    "slotDetails": {
      "slot name": {
        "resolutions" : [
          { "value": "resolved value" },
          { "value": "resolved value" }
        ],
        "originalValue": "original text"
      },
      "slot name": {
        "resolutions" : [
          { "value": "resolved value" },
          { "value": "resolved value" }
        ],
        "originalValue": "original text"
      }
    },
    "confirmationStatus": "None, Confirmed, or Denied (intent confirmation, if configured)"
  },
  "alternativeIntents": [
    {
      "name": "intent-name",
      "nluIntentConfidenceScore": score,
      "slots": {
        "slot name": "value",
        "slot name": "value"
      },
      "slotDetails": {
        "slot name": {
          "resolutions" : [
            { "value": "resolved value" },
            { "value": "resolved value" }
          ],
          "originalValue": "original text"
        },
        "slot name": {
          "resolutions" : [
            { "value": "resolved value" },
            { "value": "resolved value" }
          ],
          "originalValue": "original text"
        }
      },
      "confirmationStatus": "None, Confirmed, or Denied (intent confirmation, if configured)"
    }
  ],
  "bot": {
    "name": "bot name",
    "alias": "bot alias",
    "version": "bot version"
  },
  "userId": "User ID specified in the POST request to Amazon Lex.",
  "inputTranscript": "Text used to process the request",
  "invocationSource": "FulfillmentCodeHook or DialogCodeHook",
  "outputDialogMode": "Text or Voice, based on ContentType request header in runtime API request",
  "messageVersion": "1.0",
  "sessionAttributes": { 
     "key": "value",
     "key": "value"
  },
  "requestAttributes": { 
     "key": "value",
     "key": "value"
  },
  "recentIntentSummaryView": [
    {
        "intentName": "Name",
        "checkpointLabel": Label,
        "slots": {
          "slot name": "value",
          "slot name": "value"
        },
        "confirmationStatus": "None, Confirmed, or Denied (intent confirmation, if configured)",
        "dialogActionType": "ElicitIntent, ElicitSlot, ConfirmIntent, Delegate, or Close",
        "fulfillmentState": "Fulfilled or Failed",
        "slotToElicit": "Next slot to elicit"
    }
  ],
   "sentimentResponse": { 
      "sentimentLabel": "sentiment",
      "sentimentScore": "score"
   },
   "kendraResponse": {
       Complete query response from Amazon Kendra
   }
}
```

Note the following additional information about the event fields:
+ **currentIntent** – Provides the intent `name`, `slots`, `slotDetails` and `confirmationStatus` fields\.

   

  `nluIntentConfidenceScore` is the confidence that Amazon Lex has that the current intent is the one that best matches the user's current intent\.

   

  `slots` is a map of slot names, configured for the intent, to slot values that Amazon Lex has recognized in the user conversation\. A slot value remains null until the user provides a value\. 

   

  The slot value in the input event may not match one of the values configured for the slot\. For example, if the user responds to the prompt "What color car would you like?" with "pizza," Amazon Lex will return "pizza" as the slot value\. Your function should validate the values to make sure that they make sense in context\.

   

  `slotDetails` provides additional information about a slot value\. The `resolutions` array contains a list of additional values recognized for the slot\. Each slot can have a maximum of five values\.

   

  The `originalValue` field contains the value that was entered by the user for the slot\. When the slot type is configured to return the top resolution value as the slot value, the `originalValue` may be different from the value in the `slots` field\.

   

  `confirmationStatus` provides the user response to a confirmation prompt, if there is one\. For example, if Amazon Lex asks "Do you want to order a large cheese pizza?," depending on the user response, the value of this field can be `Confirmed` or `Denied`\. Otherwise, this value of this field is `None`\. 

   

  If the user confirms the intent, Amazon Lex sets this field to `Confirmed`\. If the user denies the intent, Amazon Lex sets this value to `Denied`\.

   

  In the confirmation response, a user utterance might provide slot updates\. For example, the user might say "yes, change size to medium\." In this case, the subsequent Lambda event has the updated slot value, `PizzaSize` set to `medium`\. Amazon Lex sets the `confirmationStatus` to `None`, because the user modified some slot data, requiring the Lambda function to perform user data validation\.

   
+ **alternativeIntents** – If you enable confidence scores, Amazon Lex returns up to four alternative intents\. Each intent includes a score that indicates the level of confidence that Amazon Lex has that the intent is the correct intent based on the user's utterance\. 

   

  The contents of the alternative intents is the same as the contents of the `currentIntent` field\. For more information, see [Using Confidence Scores](confidence-scores.md)\.

   
+ **bot** – Information about the bot that processed the request\.
  + `name` – The name of the bot that processed the request\.
  + `alias` – The alias of the bot version that processed the request\.
  + `version` – The version of the bot that processed the request\.

   
+ **userId** – This value is provided by the client application\. Amazon Lex passes it to the Lambda function\. 

   
+ **inputTranscript** – The text used to process the request\.

  If the input was text, the `inputTranscript` field contains the text that was input by the user\.

   

  If the input was an audio stream, the `inputTranscript` field contains the text extracted from the audio stream\. This is the text that is actually processed to recognize intents and slot values\. 

   
+ **invocationSource** – To indicate why Amazon Lex is invoking the Lambda function, it sets this to one of the following values: 
  + `DialogCodeHook` – Amazon Lex sets this value to direct the Lambda function to initialize the function and to validate the user's data input\. 

     

    When the intent is configured to invoke a Lambda function as an initialization and validation code hook, Amazon Lex invokes the specified Lambda function on each user input \(utterance\) after Amazon Lex understands the intent\. 
**Note**  
If the intent is not clear, Amazon Lex can't invoke the Lambda function\.

     
  + `FulfillmentCodeHook` – Amazon Lex sets this value to direct the Lambda function to fulfill an intent\.

     

    If the intent is configured to invoke a Lambda function as a fulfillment code hook, Amazon Lex sets the `invocationSource` to this value only after it has all the slot data to fulfill the intent\. 

     

  In your intent configuration, you can have two separate Lambda functions to initialize and validate user data and to fulfill the intent\. You can also use one Lambda function to do both\. In that case, your Lambda function can use the `invocationSource` value to follow the correct code path\.

    
+ **outputDialogMode** – For each user input, the client sends the request to Amazon Lex using one of the runtime API operations, [PostContent](API_runtime_PostContent.md) or [PostText](API_runtime_PostText.md)\. Amazon Lex uses the request parameters to determine whether the response to the client is text or voice, and sets this field accordingly\.

   

  The Lambda function can use this information to generate an appropriate message\. For example, if the client expects a voice response, your Lambda function could return Speech Synthesis Markup Language \(SSML\) instead of text\.

   
+ **messageVersion** – The version of the message that identifies the format of the event data going into the Lambda function and the expected format of the response from a Lambda function\. 
**Note**  
You configure this value when you define an intent\. In the current implementation, only message version 1\.0 is supported\. Therefore, the console assumes the default value of 1\.0 and doesn't show the message version\.
+ **sessionAttributes** – Application\-specific session attributes that the client sends in the request\. If you want Amazon Lex to include them in the response to the client, your Lambda function should send these back to Amazon Lex in the response\. For more information, see [Setting Session Attributes](context-mgmt.md#context-mgmt-session-attribs)

   
+ **requestAttributes** – Request\-specific attributes that the client sends in the request\. Use request attributes to pass information that doesn't need to persist for the entire session\. If there are no request attributes, the value will be null\. For more information, see [Setting Request Attributes](context-mgmt.md#context-mgmt-request-attribs)

   
+ **recentIntentSummaryView** – Information about the state of an intent\. You can see information about the last three intents used\. You can use this information to set values in the intent or to return to a previous intent\. For more information, see [Managing Sessions With the Amazon Lex API](how-session-api.md)\.

   
+ **sentimentResponse** – The result of an Amazon Comprehend sentiment analysis of the last utterance\. You can use this information to manage the conversation flow of your bot depending on the sentiment expressed by the user\. For more information, see [Sentiment Analysis](sentiment-analysis.md)\. 

   
+ **kendraResponse** – The result of a query to an Amazon Kendra index\. Only present in the input to a fulfillment code hook and only when the intent extends the `AMAZON.KendraSearchIntent` built\-in intent\. The field contains the entire response from the Amazon Kendra search\. For more information, see [AMAZON\.KendraSearchIntent](built-in-intent-kendra-search.md)\.

## Response Format<a name="using-lambda-response-format"></a>

Amazon Lex expects a response from a Lambda function in the following format:

```
{
    "sessionAttributes": {
    "key1": "value1",
    "key2": "value2"
    ...
  },
  "recentIntentSummaryView": [
    {
       "intentName": "Name",
       "checkpointLabel": "Label",
       "slots": {
         "slot name": "value",
         "slot name": "value"
        },
       "confirmationStatus": "None, Confirmed, or Denied (intent confirmation, if configured)",
        "dialogActionType": "ElicitIntent, ElicitSlot, ConfirmIntent, Delegate, or Close",
        "fulfillmentState": "Fulfilled or Failed",
        "slotToElicit": "Next slot to elicit"
    }
  ],
  "dialogAction": {
    "type": "ElicitIntent, ElicitSlot, ConfirmIntent, Delegate, or Close",
    Full structure based on the type field. See below for details.
  }
}
```

The response consists of three fields\. The `sessionAttributes` and `recentIntentSummaryView` fields are optional, the `dialogAction` field is required\. The contents of the `dialogAction` field depends on the value of the `type` field\. For details, see [dialogAction](#lambda-response-dialogAction)\.

### sessionAttributes<a name="lambda-response-sessionAttributes"></a>

Optional\. If you include the `sessionAttributes` field it can be empty\. If your Lambda function doesn't return session attributes, the last known `sessionAttributes` passed via the API or Lambda function remain\. For more information, see the [PostContent](API_runtime_PostContent.md) and [PostText](API_runtime_PostText.md) operations\.

```
  "sessionAttributes": { 
     "key1": "value1",
     "key2": "value2"
  }
```

### recentIntentSummaryView<a name="lambda-response-recentIntentSummaryView"></a>

Optional\. If included, sets values for one or more recent intents\. You can include information for up to three intents\. For example, you can set values for previous intents based on information gathered by the current intent\. The information in the summary must be valid for the intent\. For example, the intent name must be an intent in the bot\. If you include a slot value in the summary view, the slot must exist in the intent\. If you don't include the `recentIntentSummaryView` in your response, all of the values for the recent intents remain unchanged\. For more information, see the [PutSession](API_runtime_PutSession.md) operation or the [IntentSummary](API_runtime_IntentSummary.md) data type\.

```
"recentIntentSummaryView": [
    {
       "intentName": "Name",
       "checkpointLabel": "Label",
       "slots": {
         "slot name": "value",
         "slot name": "value"
        },
       "confirmationStatus": "None, Confirmed, or Denied (intent confirmation, if configured)",
        "dialogActionType": "ElicitIntent, ElicitSlot, ConfirmIntent, Delegate, or Close",
        "fulfillmentState": "Fulfilled or Failed",
        "slotToElicit": "Next slot to elicit"
    }
  ]
```

### dialogAction<a name="lambda-response-dialogAction"></a>

Required\. The `dialogAction` field directs Amazon Lex to the next course of action, and describes what to expect from the user after Amazon Lex returns a response to the client\.

The `type` field indicates the next course of action\. It also determines the other fields that the Lambda function needs to provide as part of the `dialogAction` value\.
+ `Close` — Informs Amazon Lex not to expect a response from the user\. For example, "Your pizza order has been placed" does not require a response\.

   

  The `fulfillmentState` field is required\. Amazon Lex uses this value to set the `dialogState` field in the [PostContent](API_runtime_PostContent.md) or [PostText](API_runtime_PostText.md) response to the client application\. The `message` and `responseCard` fields are optional\. If you don't specify a message, Amazon Lex uses the goodbye message or the follow\-up message configured for the intent\.

  ```
  "dialogAction": {
      "type": "Close",
      "fulfillmentState": "Fulfilled or Failed",
      "message": {
        "contentType": "PlainText or SSML or CustomPayload",
        "content": "Message to convey to the user. For example, Thanks, your pizza has been ordered."
      },
     "responseCard": {
        "version": integer-value,
        "contentType": "application/vnd.amazonaws.card.generic",
        "genericAttachments": [
            {
               "title":"card-title",
               "subTitle":"card-sub-title",
               "imageUrl":"URL of the image to be shown",
               "attachmentLinkUrl":"URL of the attachment to be associated with the card",
               "buttons":[ 
                   {
                      "text":"button-text",
                      "value":"Value sent to server on button click"
                   }
                ]
             } 
         ] 
       }
    }
  ```
+ `ConfirmIntent` — Informs Amazon Lex that the user is expected to give a yes or no answer to confirm or deny the current intent\.

   

  You must include the `intentName` and `slots` fields\. The `slots` field must contain an entry for each of the filled slots for the specified intent\. You don't need to include a entry in the `slots` field for slots that aren't filled\. You must include the `message` field if the intent's `confirmationPrompt` field is null\. The contents of the `message` field returned by the Lambda function take precedence over the `confirmationPrompt` specified in the intent\. The `responseCard` field is optional\. 

  ```
  "dialogAction": {
      "type": "ConfirmIntent",
      "message": {
        "contentType": "PlainText or SSML or CustomPayload",
        "content": "Message to convey to the user. For example, Are you sure you want a large pizza?"
      },
     "intentName": "intent-name",
     "slots": {
        "slot-name": "value",
        "slot-name": "value",
        "slot-name": "value"  
     },
     "responseCard": {
        "version": integer-value,
        "contentType": "application/vnd.amazonaws.card.generic",
        "genericAttachments": [
            {
               "title":"card-title",
               "subTitle":"card-sub-title",
               "imageUrl":"URL of the image to be shown",
               "attachmentLinkUrl":"URL of the attachment to be associated with the card",
               "buttons":[ 
                   {
                      "text":"button-text",
                      "value":"Value sent to server on button click"
                   }
                ]
             } 
         ] 
       }
    }
  ```
+ `Delegate` — Directs Amazon Lex to choose the next course of action based on the bot configuration\. If the response does not include any session attributes Amazon Lex retains the existing attributes\. If you want a slot value to be null, you don't need to include the slot field in the request\. You will get a `DependencyFailedException` exception if your fulfillment function returns the `Delegate` dialog action without removing any slots\.

  The `kendraQueryRequestPayload` and `kendraQueryFilterString` fields are optional and only used when the intent is derived from the `AMAZON.KendraSearchIntent` built\-in intent\. for more information, see [AMAZON\.KendraSearchIntent](built-in-intent-kendra-search.md)\.

  ```
    "dialogAction": {
     "type": "Delegate",
     "slots": {
        "slot-name": "value",
        "slot-name": "value",
        "slot-name": "value"  
     },
     "kendraQueryRequestPayload": "Amazon Kendra query",
     "kendraQueryFilterString": "Amazon Kendra attribute filters"
    }
  ```
+ `ElicitIntent` — Informs Amazon Lex that the user is expected to respond with an utterance that includes an intent\. For example, "I want a large pizza," which indicates the `OrderPizzaIntent`\. The utterance "large," on the other hand, is not sufficient for Amazon Lex to infer the user's intent\.

   

  The `message` and `responseCard` fields are optional\. If you don't provide a message, Amazon Lex uses one of the bot's clarification prompts\. If there is no clarification prompt defined, Amazon Lex returns a 400 Bad Request exception\.

  ```
  {
    "dialogAction": {
      "type": "ElicitIntent",
      "message": {
        "contentType": "PlainText or SSML or CustomPayload",
        "content": "Message to convey to the user. For example, What can I help you with?"
      },
      "responseCard": {
        "version": integer-value,
        "contentType": "application/vnd.amazonaws.card.generic",
        "genericAttachments": [
            {
               "title":"card-title",
               "subTitle":"card-sub-title",
               "imageUrl":"URL of the image to be shown",
               "attachmentLinkUrl":"URL of the attachment to be associated with the card",
               "buttons":[ 
                   {
                      "text":"button-text",
                      "value":"Value sent to server on button click"
                   }
                ]
             } 
         ] 
      }
   }
  ```
+ `ElicitSlot` — Informs Amazon Lex that the user is expected to provide a slot value in the response\.

   

  The `intentName`, `slotToElicit`, and `slots` fields are required\. The `message` and `responseCard` fields are optional\. If you don't specify a message, Amazon Lex uses one of the slot elicitation prompts configured for the slot\. 

  ```
    "dialogAction": {
      "type": "ElicitSlot",
      "message": {
        "contentType": "PlainText or SSML or CustomPayload",
        "content": "Message to convey to the user. For example, What size pizza would you like?"
      },
     "intentName": "intent-name",
     "slots": {
        "slot-name": "value",
        "slot-name": "value",
        "slot-name": "value"  
     },
     "slotToElicit" : "slot-name",
     "responseCard": {
        "version": integer-value,
        "contentType": "application/vnd.amazonaws.card.generic",
        "genericAttachments": [
            {
               "title":"card-title",
               "subTitle":"card-sub-title",
               "imageUrl":"URL of the image to be shown",
               "attachmentLinkUrl":"URL of the attachment to be associated with the card",
               "buttons":[ 
                   {
                      "text":"button-text",
                      "value":"Value sent to server on button click"
                   }
                ]
             } 
         ] 
       }
    }
  ```