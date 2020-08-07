# ConversationLogsRequest<a name="API_ConversationLogsRequest"></a>

Provides the settings needed for conversation logs\.

## Contents<a name="API_ConversationLogsRequest_Contents"></a>

 **iamRoleArn**   <a name="lex-Type-ConversationLogsRequest-iamRoleArn"></a>
The Amazon Resource Name \(ARN\) of an IAM role with permission to write to your CloudWatch Logs for text logs and your S3 bucket for audio logs\. If audio encryption is enabled, this role also provides access permission for the AWS KMS key used for encrypting audio logs\. For more information, see [Creating an IAM Role and Policy for Conversation Logs](https://docs.aws.amazon.com/lex/latest/dg/conversation-logs-role-and-policy.html)\.  
Type: String  
Length Constraints: Minimum length of 20\. Maximum length of 2048\.  
Pattern: `^arn:[\w\-]+:iam::[\d]{12}:role/.+$`   
Required: Yes

 **logSettings**   <a name="lex-Type-ConversationLogsRequest-logSettings"></a>
The settings for your conversation logs\. You can log the conversation text, conversation audio, or both\.  
Type: Array of [LogSettingsRequest](API_LogSettingsRequest.md) objects  
Required: Yes

## See Also<a name="API_ConversationLogsRequest_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/lex-models-2017-04-19/ConversationLogsRequest) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/lex-models-2017-04-19/ConversationLogsRequest) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/lex-models-2017-04-19/ConversationLogsRequest) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/lex-models-2017-04-19/ConversationLogsRequest) 