# Creating an IAM Role and Policies for Conversation Logs<a name="conversation-logs-role-and-policy"></a>

To enable conversation logs, you must grant write permission for CloudWatch Logs and Amazon S3\. If you enable object encryption for your S3 objects, you need to grant access permission to the AWS KMS keys used to encrypt the objects\. 

You can use the IAM console, the IAM API, or the AWS Command Line Interface to create the role and policies\. These instructions use the AWS CLI to create the role and policies\.

**Note**  
The following code is formatted for Linux and MacOS\. For Windows, replace the Linux line continuation character \(\\\) with a caret \(^\)\.

**To create an IAM role for conversation logs**

1. Create a document in the current directory called **LexConversationLogsAssumeRolePolicyDocument\.json**, add the following code to it, and save it\.

   ```
   {
     "Version": "2012-10-17",
     "Statement": [
       {
         "Effect": "Allow",
         "Principal": {
           "Service": "lex.amazonaws.com"
         },
         "Action": "sts:AssumeRole"
       }
     ]
   }
   ```

1. In the AWS CLI, run the following command to create the IAM role for conversation logs\.

   ```
   aws iam create-role \
       --role-name role-name \
       --assume-role-policy-document file://LexConversationLogsAssumeRolePolicyDocument.json
   ```

Next, create and attach a policy to the role that enables Amazon Lex to write to CloudWatch Logs\. 

**To create an IAM policy for logging conversation text to CloudWatch Logs**

1. Create a document in the current directory called **LexConversationLogsCloudWatchLogsPolicy\.json**, add the following IAM policy to it, and save it\.

   ```
   {
     "Version": "2012-10-17",
     "Statement": [
         {
             "Effect": "Allow",
             "Action": [
                 "logs:CreateLogStream",
                 "logs:PutLogEvents"
             ],
             "Resource": "arn:aws:logs:region:account-id:log-group:log-group-name:*"
         }
     ]
   }
   ```

1. In the AWS CLI, create the IAM policy that grants write permission to the CloudWatch Logs log group\.

   ```
   aws iam create-policy \
       --policy-name cloudwatch-policy-name \
       --policy-document file://LexConversationLogsCloudWatchLogsPolicy.json
   ```

1. Attach the policy to the IAM role that you created for conversation logs\.

   ```
   aws iam attach-role-policy \
       --policy-arn arn:aws:iam::account-id:policy/cloudwatch-policy-name \
       --role-name role-name
   ```

If you are logging audio to an S3 bucket, create a policy that enables Amazon Lex to write to the bucket\.

**To create an IAM policy for audio logging to an S3 bucket**

1. Create a document in the current directory called **LexConversationLogsS3Policy\.json**, add the following policy to it, and save it\.

   ```
   {
     "Version": "2012-10-17",
     "Statement": [
         {
             "Effect": "Allow",
             "Action": [
                 "s3:PutObject"
             ],
             "Resource": "arn:aws:s3:::bucket-name/*"
         }
     ]
   }
   ```

1. In the AWS CLI, create the IAM policy that grants write permission to your S3 bucket\.

   ```
   aws iam create-policy \
       --policy-name s3-policy-name \
       --policy-document file://LexConversationLogsS3Policy.json
   ```

1. Attach the policy to the role that you created for conversation logs\.

   ```
   aws iam attach-role-policy \
       --policy-arn arn:aws:iam::account-id:policy/s3-policy-name \
       --role-name role-name
   ```