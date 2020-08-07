# Using Confidence Scores<a name="confidence-scores"></a>

When a user makes an utterance, Amazon Lex uses natural language understanding \(NLU\) to understand the user's request and return the proper intent\. By default, Amazon Lex returns the most likely intent defined by your bot\.

In some cases it may be difficult for Amazon Lex to determine the most likely intent\. For example, the user might make an ambiguous utterance, or there might be two intents that are similar\. To help determine the proper intent, you can combine your domain knowledge with the *confidence scores* of a list of alternative intents\. A confidence score is a rating that Amazon Lex provides that shows how confident it is that an intent is the correct intent\.

To determine the difference between two alternative intents, you can compare their confidence scores\. For example, if one intent has a confidence score of 0\.95 and another has a score of 0\.65, the first intent is probably correct\. However, if one intent has a score of 0\.75 and another has a score of 0\.72, there is ambiguity between the two intents that you may be able to discriminate using domain knowledge in your application\.

You can also use confidence scores to create test applications that determine if changes to an intent's utterances make a difference in the behavior of the bot\. For example, you can get the confidence scores for a bot's intents using a set of utterances, then update the intents with new utterances\. You can then check the confidence scores to see if there was an improvement\.

The confidence scores that Amazon Lex returns are comparative values\. You should not rely on them as an absolute score\. The values may change based on improvements to Amazon Lex\.

When you use confidence scores, Amazon Lex returns the most likely intent and up to 4 alternative intents with their associated scores in each response\. If all of the confidence scores are less than a threshold, Amazon Lex includes the `AMAZON.FallbackIntent`, the `AMAZON.KendraSearchIntent`, or both, if you have them configured\. You can use the default threshold or you can set your own threshold\.

The following JSON code shows the `alternativeIntents` field in the response from the [PostText](API_runtime_PostText.md) operation\.

```
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
```

Set the threshold when you create or update a bot\. You can use either the API or the Amazon Lex console\. For the regions listed below you need to opt\-in to enable accuracy improvements and confidence scores\. In the console, choose confidence scores in the **Advanced Options** section\. Using the API, set the `enableModelImprovements` parameter when you call the [PutBot](API_PutBot.md) operation\. :
+ US East \(N\. Virginia\) \(us\-east\-1\)
+ US West \(Oregon\) \(us\-west\-2\)
+ Asia Pacific \(Sydney\) \(ap\-southeast\-2\)
+ Europe \(Ireland\) \(eu\-west\-1\)

In all other regions, accuracy improvements and confidence score support is available by default\.

To change the confidence threshold, set it in the console or using the [PutBot](API_PutBot.md) operation\. The threshold must be a number between 1\.00 and 0\.00\.

To use the console, set the confidence threshold when you create or update your bot\.

**To set the confidence threshold when creating a bot \(Console\)**
+ On **Create your bot**, enter a value in the **Confidence score threshold** field\.

**To update the confidence threshold \(Console\)**

1. From the list of your bots, choose the bot to update\.

1. Choose the **Settings** tab\.

1. In the left navigation, choose **General**\.

1. Update the value in the **Confidence score threshold** field\.

**To set or update the confidence threshold \(SDK\)**
+ Set the `nluIntentConfidenceThreshold` parameter of the [PutBot](API_PutBot.md) operation\. The following JSON code shows the parameter being set\.

  ```
     "nluIntentConfidenceThreshold": 0.75,
  ```

## Session Management<a name="confidence-scores-session-management"></a>

To change the intent that Amazon Lex uses in a conversation with the user, you can use the response from your dialog code hook Lambda function, or you can use the session management APIs in your custom application\. 

### Using a Lambda function<a name="session-management-lambda"></a>

When you use a Lambda function, Amazon Lex calls it with a JSON structure that contains the input to the function\. The JSON structure contains a field called `currentIntent` that contains the intent that Amazon Lex has identified as the most likely intent for the user's utterance\. The JSON structure also includes an `alternativeIntents` field that contains up to four additional intents that may satisfy the user's intent\. Each intent includes a field called `nluIntentConfidenceScore` that contains the confidence score that Amazon Lex assigned to the intent\.

To use an alternative intent, you specify it in the `ConfirmIntent` or the `ElicitSlot` dialog action in your Lambda function\.

For more information, see [Using Lambda Functions](using-lambda.md)\.

### Using the Session Management API<a name="session-management-API"></a>

To use a different intent from the current intent, use the [PutSession](API_runtime_PutSession.md) operation\. For example, if you decide that the first alternative is preferable to the intent that Amazon Lex chose, you can use the `PutSession` operation to change intents so that the next intent that the user interacts with is the one that you selected\.

For more information, see [Managing Sessions With the Amazon Lex API](how-session-api.md)\.