# ConversationLogsResponse<a name="API_ConversationLogsResponse"></a>

Contains information about conversation log settings\.

## Contents<a name="API_ConversationLogsResponse_Contents"></a>

 **iamRoleArn**   <a name="lex-Type-ConversationLogsResponse-iamRoleArn"></a>
The Amazon Resource Name \(ARN\) of the IAM role used to write your logs to CloudWatch Logs or an S3 bucket\.  
Type: String  
Length Constraints: Minimum length of 20\. Maximum length of 2048\.  
Pattern: `^arn:[\w\-]+:iam::[\d]{12}:role/.+$`   
Required: No

 **logSettings**   <a name="lex-Type-ConversationLogsResponse-logSettings"></a>
The settings for your conversation logs\. You can log text, audio, or both\.  
Type: Array of [LogSettingsResponse](API_LogSettingsResponse.md) objects  
Required: No

## See Also<a name="API_ConversationLogsResponse_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/lex-models-2017-04-19/ConversationLogsResponse) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/lex-models-2017-04-19/ConversationLogsResponse) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/lex-models-2017-04-19/ConversationLogsResponse) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/lex-models-2017-04-19/ConversationLogsResponse) 