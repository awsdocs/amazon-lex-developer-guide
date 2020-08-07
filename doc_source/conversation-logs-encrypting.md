# Encrypting Conversation Logs<a name="conversation-logs-encrypting"></a>

You can use encryption to help protect the contents of your conversation logs\. For text and audio logs, you can use AWS KMS customer managed CMKs to encrypt data in your CloudWatch Logs log group and S3 bucket\.

**Note**  
Amazon Lex supports only symmetric CMKs\. Do not use an asymmetric CMK to encrypt your data\.

You enable encryption using an AWS KMS key on the CloudWatch Logs log group that Amazon Lex uses for text logs\. You can't provide an AWS KMS key in the log settings to enable AWS KMS encryption of your log group\. For more information, see [ Encrypt Log Data in CloudWatch Logs Using AWS KMS ](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/encrypt-log-data-kms.html) in the *Amazon CloudWatch Logs User Guide*\.

For audio logs you use default encryption on your S3 bucket or specify an AWS KMS key to encrypt your audio objects\. Even if your S3 bucket uses default encryption you can still specify a different AWS KMS key to encrypt your audio objects\. For more information, see [ Amazon S3 Default Encryption for S3 Buckets ](https://docs.aws.amazon.com/AmazonS3/latest/dev/bucket-encryption.html) in the *Amazon Simple Storage Service Developer Guide*\.

Amazon Lex requires AWS KMS permissions if you choose to encrypt your audio logs\. You need to attach additional policies to the IAM role used for conversation logs\. If you use default encryption on your S3 bucket, your policy must grant access to the AWS KMS key configured for that bucket\. If you specify an AWS KMS key in your audio log settings, your must grant access to that key\.

If you have not created a role for conversation logs, see [IAM Policies for Conversation Logs](conversation-logs-policies.md)\.

**To create an IAM policy for using an AWS KMS key for encrypting audio logs**

1. Create a document in the current directory called **LexConversationLogsKMSPolicy\.json**, add the following policy to it, and save it\.

   ```
   {
     "Version": "2012-10-17",
     "Statement": [
         {
             "Effect": "Allow",
             "Action": [
                 "kms:GenerateDataKey"
             ],
             "Resource": "kms-key-arn"
         }
     ]
   }
   ```

1. In the AWS CLI, create the IAM policy that grants permission to use the AWS KMS key for encrypting audio logs\.

   ```
   aws iam create-policy \
       --policy-name kms-policy-name \
       --policy-document file://LexConversationLogsKMSPolicy.json
   ```

1. Attach the policy to the role that you created for conversation logs\.

   ```
   aws iam attach-role-policy \
       --policy-arn arn:aws:iam::account-id:policy/kms-policy-name \
       --role-name role-name
   ```