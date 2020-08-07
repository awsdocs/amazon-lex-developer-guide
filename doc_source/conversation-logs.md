# Conversation Logs<a name="conversation-logs"></a>

You enable *conversation logs* to store bot interactions\. You can use these logs to review the performance of your bot and to troubleshoot issues with conversations\. You can log text for the [PostText](API_runtime_PostText.md) operation\. You can log both text and audio for the [PostContent](API_runtime_PostContent.md) operation\. By enabling conversation logs you get a detailed view of conversations that users have with your bot\.

For example, a session with your bot has a session ID\. You can use this ID to get the transcript of the conversation including user utterances and the corresponding bot responses\. You also get metadata such as intent name and slot values for an utterance\.

**Note**  
You can't use conversation logs with a bot subject to the Children's Online Privacy Protection Act \(COPPA\)\.

Conversation logs are configured for an alias\. Each alias can have different settings for their text and audio logs\. You can enable text logs, audio logs, or both for each alias\. Text logs store text input, transcripts of audio input, and associated metadata in CloudWatch Logs\. Audio logs store audio input in Amazon S3\. You can enable encryption of text and audio logs using AWS KMS customer managed CMKs\.

To configure logging, use the console or the [PutBotAlias](API_PutBotAlias.md) operation\. You can't log conversations for the `$LATEST` alias of your bot or for the test bot available in the Amazon Lex console\. After enabling conversation logs for an alias, [PostContent](API_runtime_PostContent.md) or [PostText](API_runtime_PostText.md) operation for that alias logs the text or audio utterances in the configured CloudWatch Logs log group or S3 bucket\.

**Topics**
+ [IAM Policies for Conversation Logs](conversation-logs-policies.md)
+ [Configuring Conversation Logs](conversation-logs-configure.md)
+ [Encrypting Conversation Logs](conversation-logs-encrypting.md)
+ [Viewing Text Logs in Amazon CloudWatch Logs](conversation-logs-cw.md)
+ [Accessing Audio Logs in Amazon S3](conversation-logs-s3.md)
+ [Monitoring Conversation Log Status with CloudWatch Metrics](conversation-logs-monitoring.md)