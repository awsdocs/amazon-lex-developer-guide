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
   "sessionId": "session ID"
}
```

The `intent` and `slots` fields may not appear in an entry if a missed utterance doesn't get mapped to an intent\. The `s3PathForAudio` field doesn't appear if audio logs are disabled or if the `inputDialogMode`field is `Text`\.

**Note**  
The input format may change without a corresponding change in the `messageVersion`\. Your code should not throw an error if new fields are present\.

You must have a role and policy set to enable Amazon Lex to write to CloudWatch Logs\. For more information see [Creating an IAM Role and Policies for Conversation Logs](conversation-logs-role-and-policy.md)\.