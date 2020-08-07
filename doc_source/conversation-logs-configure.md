# Configuring Conversation Logs<a name="conversation-logs-configure"></a>

You enable and disable conversation logs using the console or the `conversationLogs` field of the `PutBotAlias` operation\. You can turn on or turn off audio logs, text logs, or both\. Logging starts on new bot sessions\. Changes to log settings aren't reflected for active sessions\.

To store text logs, use an Amazon CloudWatch Logs log group in your AWS account\. You can use any valid log group\. The log group must be in the same region as the Amazon Lex bot\. For more information about creating a CloudWatch Logs log group, see [ Working with Log Groups and Log Streams ](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/Working-with-log-groups-and-streams.html) in the *Amazon CloudWatch Logs User Guide*\.

To store audio logs, use an Amazon S3 bucket in your AWS account\. You can use any valid S3 bucket\. The bucket must be in the same region as the Amazon Lex bot\. For more information about creating an S3 bucket, see [ Create a Bucket ](https://docs.aws.amazon.com/AmazonS3/latest/gsg/CreatingABucket.html) in the *Amazon Simple Storage Service Getting Started Guide*\.

You must provide an IAM role with policies that enable Amazon Lex to write to the configured log group or bucket\. For more information, see [Creating an IAM Role and Policies for Conversation Logs](conversation-logs-policies.md#conversation-logs-role-and-policy)\.

The IAM role that you use to enable conversation logs must have the `iam:PassRole` permission\. The following policy should be attached to the role\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "iam:PassRole",
            "Resource": "arn:aws:iam::account:role/role"
        }
    ]
}
```

## Enabling Conversation Logs<a name="conversation-logs-enable"></a>

**To turn on logs using the console**

1. Open the Amazon Lex console [https://console\.aws\.amazon\.com/lex](https://console.aws.amazon.com/lex)\.

1. From the list, choose a bot\.

1. Choose the **Settings** tab, and then from the left menu choose **Conversation logs**\.

1. In the list of aliases, choose the settings icon for the alias for which you want to configure conversation logs\.

1. Select whether to log text, audio, or both\. 

1. For text logging, enter the Amazon CloudWatch Logs log group name\.

1. For audio logging, enter the S3 bucket information\.

1. Optional\. To encrypt audio logs, choose the AWS KMS key to use for encryption\.

1. Choose an IAM role with the required permissions\.

1. Choose **Save** to start logging conversations\.

**To turn on text logs using the API**

1. Call the [PutBotAlias](API_PutBotAlias.md) operation with an entry in the `logSettings` member of the `conversationLogs` field
   + Set the `destination` member to `CLOUDWATCH_LOGS`
   + Set the `logType` member to `TEXT`
   + Set the `resourceArn` member to the Amazon Resource Name \(ARN\) of the CloudWatch Logs log group that is the destination for the logs

1. Set the `iamRoleArn` member of the `conversationLogs` field to the Amazon Resource Name \(ARN\) of an IAM role that has the required permissions for enabling conversation logs on the specified resources\.

**To turn on audio logs using the API**

1. Call the [PutBotAlias](API_PutBotAlias.md) operation with an entry in the `logSettings` member of the `conversationLogs` field
   + Set the `destination` member to `S3`
   + Set the `logType` member to `AUDIO`
   + Set the `resourceArn` member to the ARN of the Amazon S3 bucket where the audio logs are stored
   + Optional\. To encrypt audio logs with a specific AWS KMS key, set the `kmsKeyArn` member of the ARN of the key that is used for encryption\.

1. Set the `iamRoleArn` member of the `conversationLogs` field to the Amazon Resource Name \(ARN\) of an IAM role that has the required permissions for enabling conversation logs on the specified resources\.

## Disabling Conversation Logs<a name="conversation-logs-disable"></a>

**To turn off logs using the console**

1. Open the Amazon Lex console [https://console\.aws\.amazon\.com/lex](https://console.aws.amazon.com/lex)\.

1. From the list, choose a bot\.

1. Choose the **Settings** tab, and then from the left menu choose **Conversation logs**\.

1. In the list of aliases, choose the settings icon for the alias for which you want to configure conversation logs\.

1. Clear the check from text, audio, or both to turn off logging\.

1. Choose **Save** to stop logging conversations\.

**To turn off logs using the API**
+ Call the `PutBotAlias` operation without the `conversationLogs` field\.

**To turn off text logs using the API**
+ 
  + If you are logging audio
    + Call the [PutBotAlias](API_PutBotAlias.md) operation with a `logSettings` entry only for `AUDIO`\.
    + The call to the `PutBotAlias` operation must not have a `logSettings` entry for `TEXT`\.
  + If you are not logging audio
    + Call the [PutBotAlias](API_PutBotAlias.md) operation without the `conversationLogs` field\.

**To turn off audio logs using the API**
+ 
  + If you are logging text
    + Call the [PutBotAlias](API_PutBotAlias.md) operation with a `logSettings` entry only for `TEXT`\.
    + The call to the `PutBotAlias` operation must not have a `logSettings` entry for `AUDIO`\.
  + If you are not logging text
    + Call the [PutBotAlias](API_PutBotAlias.md) operation without the `conversationLogs` field\.