# Accessing Audio Logs in Amazon S3<a name="conversation-logs-s3"></a>

Amazon Lex stores audio logs for your conversations in an S3 bucket\. 

**To access audio logs using the console**

1. Open the Amazon Lex console [https://console\.aws\.amazon\.com/lex](https://console.aws.amazon.com/lex)\.

1. From the list, choose a bot\.

1. Choose the **Settings** tab, then from the left menu choose **Conversation logs**\.

1. Choose the link under **Audio logs** to access the logs for the alias in the Amazon S3 console\.

You can also use the Amazon S3 console or API to access audio logs\. You can see the S3 object key prefix of the audio files in the Amazon Lex console, or in the `resourcePrefix` field in the `GetBotAlias` operation response\.