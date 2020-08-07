# Monitoring Conversation Log Status with CloudWatch Metrics<a name="conversation-logs-monitoring"></a>

Use Amazon CloudWatch to monitor delivery metrics of your conversation logs\. You can set alarms on metrics so that you are aware of issues with logging if they should occur\.

Amazon Lex provides four metrics in the `AWS/Lex` namespace for conversation logs:
+ `ConversationLogsAudioDeliverySuccess`
+ `ConversationLogsAudioDeliveryFailure`
+ `ConversationLogsTextDeliverySuccess`
+ `ConversationLogsTextDeliveryFailure`

For more information, see [CloudWatch Metrics for Conversation Logs](monitoring-aws-lex-cloudwatch.md#cloudwatch-metrics-for-logging)\.

The success metrics show that Amazon Lex has successfully written your audio or text logs to their destinations\. 

The failure metrics show that Amazon Lex couldn't deliver audio or text logs to the specified destination\. Typically, this is a configuration error\. When your failure metrics are above zero, check the following:
+ Make sure that Amazon Lex is a trusted entity for the IAM role\.
+ For text logging, make sure that the CloudWatch Logs log group exists\. For audio logging, make sure that the S3 bucket exists\.
+ Make sure that the IAM role that Amazon Lex uses to access the CloudWatch Logs log group or S3 bucket has write permission for the log group or bucket\.
+ Make sure that the S3 bucket exists in the same region as the Amazon Lex bot and belongs to your account\.
+ If you are using an AWS KMS key for S3 encryption, make sure that there are no policies that prevent Amazon Lex from using your key and make sure that the IAM role you provide has the necessary AWS KMS permissions\. For more information, see [IAM Policies for Conversation Logs](conversation-logs-policies.md)\.