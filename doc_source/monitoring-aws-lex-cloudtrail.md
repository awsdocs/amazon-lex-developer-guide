# Monitoring Amazon Lex API Calls with AWS CloudTrail Logs<a name="monitoring-aws-lex-cloudtrail"></a>

Amazon Lex is integrated with AWS CloudTrail, a service that captures all of the Amazon Lex API calls and delivers log files to an S3 bucket, where they are written with other AWS service records\. CloudTrail captures API calls from the Amazon Lex console or from Amazon Lex API operations\. Using the information collected by CloudTrail, you can track requests made to Amazon Lex, the source IP address from which the requests were made, who made the requests, when they were made, and so on\. 

Each operation creates a log entry containing request information\. Only the following operations contain response information:
+  [CreateBotVersion](API_CreateBotVersion.md), [CreateIntentVersion](API_CreateIntentVersion.md), [CreateSlotTypeVersion](API_CreateSlotTypeVersion.md)
+ [PutBot](API_PutBot.md), [PutBotAlias](API_PutBotAlias.md), [PutIntent](API_PutIntent.md), [PutSlotType](API_PutSlotType.md) 

Every log entry contains information about who generated the request\. Use the user identity in log entries to determine the following: 
+ Whether the request was made with root or IAM user credentials
+ Whether the request was made with temporary security credentials for a role or federated user
+ Whether the request was made by another AWS service

 For more information, see the [CloudTrail userIdentity Element](http://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-event-reference-user-identity.html)\.

For information about the Amazon Lex actions that are logged in CloudTrail logs, see [Amazon Lex Model Building Service](http://docs.aws.amazon.com/lex/latest/dg/API_Operations_Amazon_Lex_Model_Building_Service.html)\. For example, calls to the [PutBot](API_PutBot.md), [GetBot](API_GetBot.md), and [DeleteBot](API_DeleteBot.md) operations generate entries in the CloudTrail log\. The actions documented in [Amazon Lex Runtime Service](http://docs.aws.amazon.com/lex/latest/dg/API_Operations_Amazon_Lex_Runtime_Service.html), [PostContent](API_runtime_PostContent.md) and [PostText](API_runtime_PostText.md), are not logged\. 

Log files are stored in an S3 bucket\. CloudTrail determines when to create and write to a new file based on a time period and file size that you specify\.

You can store your log files in your S3 bucket for as long as you want\. You can also define Amazon S3 lifecycle rules to archive or delete log files automatically\. By default, your log files are encrypted with Amazon S3 server\-side encryption \(SSE\)\.

If you want to be notified when CloudTrail delivers log files, configure CloudTrail to publish Amazon SNS notifications when that happens\. For more information, see [Configuring Amazon SNS Notifications for CloudTrail](http://docs.aws.amazon.com/awscloudtrail/latest/userguide/getting_notifications_top_level.html)\.

To learn more about CloudTrail, including how to configure and enable it, see the [AWS CloudTrail User Guide](http://docs.aws.amazon.com/awscloudtrail/latest/userguide/)\.

## <a name="aws-lex-info-in-cloudtrail"></a>

You can also aggregate Amazon Lex log files from multiple AWS Regions and multiple AWS accounts into a single S3 bucket\. For more information, see [Receiving CloudTrail Log Files from Multiple Regions](http://docs.aws.amazon.com/awscloudtrail/latest/userguide/receive-cloudtrail-log-files-from-multiple-regions.html) and [Receiving CloudTrail Log Files from Multiple Accounts](http://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-receive-logs-from-multiple-accounts.html)\. 

## Example: Amazon Lex Log File Entries<a name="understanding-aws-lex-entries"></a>

CloudTrail log files can contain one or more log entries\. A log entry represents a single request from any source and includes information about the requested action, the date and time of the action, request parameters, and so on\. Log entries are not an ordered stack trace of the public API calls, so they do not appear in any specific order\. 

The following example CloudTrail log entry shows the result of a call to the `PutBot` action\.

```
    {
                "eventVersion": "1.05",
                "userIdentity": {
                    "type": "AssumedRole | FederatedUser | IAMUser | Root | SAMLUser | WebIdentityUser",
                    "principalId": "principal ID",
                    "arn": "ARN",
                    "accountId": "account ID",
                    "accessKeyId": "access key ID",
                    "userName": "user name"
                },
                "eventTime": "timestamp",
                "eventSource": "lex.amazonaws.com",
                "eventName": "PutBot",
                "awsRegion": "region",
                "sourceIPAddress": "source IP address",
                "userAgent": "user agent",
                "requestParameters": {
                    "name": "CloudTrailBot",
                    "intents": [
                        {
                            "intentVersion": "11",
                            "intentName": "TestCloudTrail"
                        }
                    ],
                    "voiceId": "Salli",
                    "childDirected": false,
                    "locale": "en-US",
                    "idleSessionTTLInSeconds": 500,
                    "processBehavior": "BUILD",
                    "description": "CloudTrail test bot",
                    "clarificationPrompt": {
                        "messages": [
                            {
                                "contentType": "PlainText",
                                "content": "I didn't understand you, what would you like to do?"
                            }
                        ],
                        "maxAttempts": 2
                    },
                    "abortStatement": {
                        "messages": [
                            {
                                "contentType": "PlainText",
                                "content": "Sorry. I'm not able to assist at this time."
                            }
                        ]
                    }
                },
                "responseElements": {
                    "voiceId": "Salli",
                    "locale": "en-US",
                    "childDirected": false,
                    "abortStatement": {
                        "messages": [
                            {
                                "contentType": "PlainText",
                                "content": "Sorry. I'm not able to assist at this time."
                            }
                        ]
                    },
                    "status": "BUILDING",
                    "createdDate": "timestamp",
                    "lastUpdatedDate": "timestamp",
                    "idleSessionTTLInSeconds": 500,
                    "intents": [
                        {
                            "intentVersion": "11",
                            "intentName": "TestCloudTrail"
                        }
                    ],
                    "clarificationPrompt": {
                        "messages": [
                            {
                                "contentType": "PlainText",
                                "content": "I didn't understand you. What would you like to do?"
                            }
                        ],
                        "maxAttempts": 2
                    },
                    "version": "$LATEST",
                    "description": "CloudTrail test bot",
                    "checksum": "checksum",
                    "name": "CloudTrailBot"
                },
                "requestID": "request ID",
                "eventID": "event ID",
                "eventType": "AwsApiCall",
                "recipientAccountId": "account ID"
            }
```