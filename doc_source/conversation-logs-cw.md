# Viewing Text Logs in Amazon CloudWatch Logs<a name="conversation-logs-cw"></a>

Amazon Lex stores text logs for your conversations in Amazon CloudWatch Logs\. To view the logs, you can use the CloudWatch Logs console or API\. For more information, see [ Search Log Data Using Filter Patterns ](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/SearchDataFilterPattern.html) and [CloudWatch Logs Insights Query Syntax](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/CWL_QuerySyntax.html) in the *Amazon CloudWatch Logs User Guide*\.

**To view logs using the Amazon Lex console**

1. Open the Amazon Lex console [https://console\.aws\.amazon\.com/lex](https://console.aws.amazon.com/lex)\.

1. From the list, choose a bot\.

1. Choose the **Settings** tab, then from the left menu choose **Conversation logs**\.

1. Choose the link under **Text logs** to view the logs for the alias in the CloudWatch console\.

You can also use the CloudWatch console or API to view your log entries\. To find the log entries, navigate to the log group that you configured for the alias\. You find the log stream prefix for your logs in the Amazon Lex console or by using the [GetBotAlias](API_GetBotAlias.md) operation\. 

Log entries for a user utterance is in multiple log streams\. An utterance in the conversation has an entry in one of the log streams with the specified prefix\. An entry in the log stream contains the following information\.

```
{
   "messageVersion": "1.0",
   "botName": "bot name",
   "botAlias": "bot alias",
   "botVersion": "bot version",
   "inputTranscript": "text used to process the request",
   "botResponse": "response from the bot",
   "intent": "matched intent",
   
   "slots": {
       "slot name": "slot value",
       "slot name": null,
       "slot name": "slot value"
       ...
   },

   "missedUtterance": true | false,
   "inputDialogMode": "Text" | "Speech",
   "requestId": "request ID",
   "s3PathForAudio": "S3 path to audio file",
   "userId": "user ID",
   "sessionId": "session ID",
   "sentimentResponse": {
       "sentimentScore": "{Positive: number, Negative: number, Neutral: number, Mixed: number}",
       "sentimentLabel": "Positive" | "Negative" | "Neutral" | "Mixed"
   },
   "slotToElicit": "slot name",
   "dialogState": "ElicitIntent" | "ConfirmIntent" | "ElicitSlot" | "Fulfilled" | "ReadyForFulfillment" | "Failed",
   "responseCard": {
       "genericAttachments": [
           ...
       ],
       "contentType": "application/vnd.amazonaws.card.generic",
       "version": 1
    },
   "locale": "locale",
   "timestamp": "ISO 8601 UTC timestamp",

   
   "sessionAttributes": {
       "attribute name": "attribute value"
       ...
    },
   "requestAttributes": {
       "attribute name": "attribute value"
       ...
    }
}
```

The contents of the log entry depends on the result of a transaction and the configuration of the bot and request\.
+ The `intent`, `slots`, and `slotToElicit` fields don't appear in an entry if the `missedUtterance` field is `true`\.
+ The `s3PathForAudio` field doesn't appear if audio logs are disabled or if the `inputDialogMode`field is `Text`\.
+ The `responseCard` field only appears when you have defined a response card for the bot\.
+ The `requestAttributes` map only appears if you have specified request attributes in the request\.
+ The `sessionAttributes` map only appears if you have specified session attributes in the request\.
+ The `sentimentResponse` map only appears if you configure the bot to return sentiment values\.

**Note**  
The input format may change without a corresponding change in the `messageVersion`\. Your code should not throw an error if new fields are present\.

You must have a role and policy set to enable Amazon Lex to write to CloudWatch Logs\. For more information see [IAM Policies for Conversation Logs](conversation-logs-policies.md)\.