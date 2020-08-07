# Monitoring Amazon Lex with Amazon CloudWatch<a name="monitoring-aws-lex-cloudwatch"></a>

To track the health of your Amazon Lex bots, use Amazon CloudWatch\. With CloudWatch, you can get metrics for individual Amazon Lex operations or for global Amazon Lex operations for your account\. You can also set up CloudWatch alarms to be notified when one or more metrics exceeds a threshold that you define\. For example, you can monitor the number of requests made to a bot over a particular time period, view the latency of successful requests, or raise an alarm when errors exceed a threshold\.

## CloudWatch Metrics for Amazon Lex<a name="aws-lex-cloudwatch-using"></a>

To get metrics for your Amazon Lex operations , you must specify the following information:
+ The metric dimension\. A *dimension* is a set of name\-value pairs that you use to identify a metric\. Amazon Lex has three dimensions: 
  + `BotAlias, BotName, Operation`
  + `BotAlias, BotName, InputMode, Operation`
  + `BotName, BotVersion, InputMode, Operation`
+ The metric name, such as `MissedUtteranceCount` or `RuntimeRequestCount`\.

You can get metrics for Amazon Lex with the AWS Management Console, the AWS CLI, or the CloudWatch API\. You can use the CloudWatch API through one of the Amazon AWS Software Development Kits \(SDKs\) or the CloudWatch API tools\. The Amazon Lex console displays graphs based on the raw data from the CloudWatch API\. 

You must have the appropriate CloudWatch permissions to monitor Amazon Lex with CloudWatch \. For more information, see [ Authentication and Access Control for Amazon CloudWatch](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/auth-and-access-control-cw.html) in the *Amazon CloudWatch User Guide*\.

## Viewing Amazon Lex Metrics<a name="aws-lex-cloudwatch-metrics"></a>

View Amazon Lex metrics using the Amazon Lex console or the CloudWatch console\.

**To view metrics \(Amazon Lex console\)**

1. Sign in to the AWS Management Console and open the Amazon Lex console at [https://console\.aws\.amazon\.com/lex/](https://console.aws.amazon.com/lex/)\.

1. From the list of bots, choose the one whose metrics you want to see\.

1. Choose **Monitoring**\. Metrics are displayed in graphs\.

**To view metrics \(CloudWatch console\)**

1. Sign in to the AWS Management Console and open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. Choose **Metrics**, choose **All Metrics**, and then choose **AWS/Lex**\.

1. Choose the dimension, choose a metric name, then choose **Add to graph**\.

1. Choose a value for the date range\. The metric count for the selected date range is displayed in the graph\.

## Creating an Alarm<a name="aws-lex-cloudwatch-alarms"></a>

A CloudWatch alarm watches a single metric over a specified time period, and performs one or more actions: sending a notification to an Amazon Simple Notification Service  \(Amazon SNS\) topic or Auto Scaling policy\. The action or actions are based on the value of the metric relative to a given threshold over a number of time periods that you specify\. CloudWatch can also send you an Amazon SNS message when the alarm changes state\. 

CloudWatch alarms invoke actions only when the state changes and has persisted for the period that you specify\.

**To set an alarm**

1. Sign in to the AWS Management Console and open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. Choose **Alarms**, and then choose **Create Alarm**\. 

1. Choose **AWS/Lex Metrics**, and then choose a metric\.

1. For **Time Range**, choose a time range to monitor, and then choose **Next**\.

1. Enter a **Name** and **Description**\.

1.  For **Whenever**, choose **>=**, and type a maximum value\.

1. If you want CloudWatch to send an email when the alarm state is reached, in the **Actions** section, for **Whenever this alarm**, choose **State is ALARM**\. For **Send notification to**, choose a mailing list or choose **New list** and create a new mailing list\.

1. Preview the alarm in the **Alarm Preview** section\. If you are satisfied with the alarm, choose **Create Alarm**\.

## CloudWatch Metrics for Amazon Lex Runtime<a name="cloudwatch-dimensions-for-aws-lex-runtime"></a>

The following table describes the Amazon Lex runtime metrics\.


| Metric | Description | 
| --- | --- | 
| KendraIndexAccessError | The number of times that Amazon Lex could not access your Amazon Kendra index\. Valid dimension for the `PostContent` operation with the `Text` or `Speech` `InputMode`: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/lex/latest/dg/monitoring-aws-lex-cloudwatch.html) Valid dimension for the `PostText` operation: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/lex/latest/dg/monitoring-aws-lex-cloudwatch.html) Unit: Count  | 
| KendraLatency | The amount of time that it takes Amazon Kendra to respond to a request from the `AMAZON.KendraSearchIntent`\.Valid dimensions for the `PostContent` operation with the `Text` or `Speech` `InputMode`: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/lex/latest/dg/monitoring-aws-lex-cloudwatch.html) Valid dimensions for the `PostText` operation: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/lex/latest/dg/monitoring-aws-lex-cloudwatch.html) Unit: Milliseconds | 
| KendraSuccess | The number of successful requests from the `AMAZON.KendraSearchIntent` to your Amazon Kendra index\.Valid dimensions for the `PostContent` operation with the `Text` or `Speech` `InputMode`: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/lex/latest/dg/monitoring-aws-lex-cloudwatch.html) Valid dimensions for the `PostText` operation: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/lex/latest/dg/monitoring-aws-lex-cloudwatch.html) Unit: Count | 
| KendraSystemErrors | The number of times that Amazon Lex couldn't query the Amazon Kendra index\. Valid dimension for the `PostContent` operation with the `Text` or `Speech` `InputMode`: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/lex/latest/dg/monitoring-aws-lex-cloudwatch.html) Valid dimension for the `PostText` operation: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/lex/latest/dg/monitoring-aws-lex-cloudwatch.html) Unit: Count  | 
| KendraThrottledEvents | The number of times Amazon Kendra throttled requests from the `AMAZON.KendraSearchIntent`\. Valid dimension for the `PostContent` operation with the `Text` or `Speech` `InputMode`: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/lex/latest/dg/monitoring-aws-lex-cloudwatch.html) Valid dimension for the `PostText` operation: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/lex/latest/dg/monitoring-aws-lex-cloudwatch.html) Unit: Count  | 
| MissedUtteranceCount |  The number of utterances that were not recognized in the specified period\. Valid dimensions for the `PostContent` operation with the `Text `or `Speech` `InputMode`: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/lex/latest/dg/monitoring-aws-lex-cloudwatch.html) Valid dimensions for the `PostText` operation: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/lex/latest/dg/monitoring-aws-lex-cloudwatch.html)  | 
| RuntimeInvalidLambdaResponses |  The number of invalid AWS Lambda \(Lambda\) responses in the specified period\. Valid dimension for the `PostContent`operation with the `Text` or `Speech` `InputMode`: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/lex/latest/dg/monitoring-aws-lex-cloudwatch.html) Valid dimension for the `PostText` operation: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/lex/latest/dg/monitoring-aws-lex-cloudwatch.html)  | 
| RuntimeLambdaErrors | The number of Lambda runtime errors in the specified period\.Valid dimension for the `PostContent` operation with the `Text `or `Speech`` InputMode` :[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/lex/latest/dg/monitoring-aws-lex-cloudwatch.html)Valid dimension for the `PostText` operation: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/lex/latest/dg/monitoring-aws-lex-cloudwatch.html)  | 
| RuntimePollyErrors |  The number of invalid Amazon Polly responses in the specified period\. Valid dimension for the `PostContent` operation with the `Text` or `Speech` `InputMode`: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/lex/latest/dg/monitoring-aws-lex-cloudwatch.html) Valid dimension for the `PostText` operation: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/lex/latest/dg/monitoring-aws-lex-cloudwatch.html)  | 
| RuntimeRequestCount |  The number of runtime requests in the specified period\. Valid dimensions for the `PostContent` operation with the `Text` or `Speech` `InputMode`: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/lex/latest/dg/monitoring-aws-lex-cloudwatch.html) Valid dimensions for the `PostText` operation: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/lex/latest/dg/monitoring-aws-lex-cloudwatch.html) Unit: Count  | 
| RuntimeSuccessfulRequestLatency |  The latency for successful requests between the time that the request was made and the response was passed back\. Valid dimensions for the `PostContent` operation with the `Text` or `Speech` `InputMode`: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/lex/latest/dg/monitoring-aws-lex-cloudwatch.html) Valid dimensions for the `PostText` operation: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/lex/latest/dg/monitoring-aws-lex-cloudwatch.html) Unit: Milliseconds  | 
| RuntimeSystemErrors |  The number of system errors in the specified period\. The response code range for a system error is 500 to 599\. Valid dimension for the `PostContent` operation with the `Text` or `Speech` `InputMode`: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/lex/latest/dg/monitoring-aws-lex-cloudwatch.html) Valid dimension for the `PostText` operation: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/lex/latest/dg/monitoring-aws-lex-cloudwatch.html) Unit: Count  | 
| RuntimeThrottledEvents |  The number of throttled requests\. Amazon Lex throttles a request when it receives more requests than the limit of transactions per second set for your account\. If the limit set for your account is frequently exceeded, you can request a limit increase\. To request an increase, see [AWS Service Limits](https://docs.aws.amazon.com/general/latest/gr/aws_service_limits.html)\.  Valid dimension for the `PostContent` operation with the `Text` or `Speech` `InputMode`: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/lex/latest/dg/monitoring-aws-lex-cloudwatch.html) Valid dimension for the `PostText` operation: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/lex/latest/dg/monitoring-aws-lex-cloudwatch.html) Unit: Count  | 
| RuntimeUserErrors |  The number of user errors in the specified period\. The response code range for a user error is 400 to 499\. Valid dimension for the `PostContent` operation with `Text` or `Speech` `InputMode`: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/lex/latest/dg/monitoring-aws-lex-cloudwatch.html) Valid dimension for the `PostText` operation: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/lex/latest/dg/monitoring-aws-lex-cloudwatch.html) Unit: Count  | 

Amazon Lex runtime metrics use the `AWS/Lex` namespace, and provide metrics in the following dimensions\. You can group metrics by dimensions in the CloudWatch console:


| Dimension | Description | 
| --- | --- | 
| BotName, BotAlias, Operation, InputMode | Groups metrics by the bot's alias, the bot's name, the operation \(PostContent\), and by whether the input was text or speech\. | 
| BotName, BotVersion, Operation, InputMode | Groups metrics by the bot's name, the version of the bot, the operation \(PostContent\), and by whether the input was text or speech\. | 
| BotName, BotVersion, Operation | Groups metrics by the bot's name, the bots version, and by the operation, PostText\. | 
| BotName, BotAlias, Operation | Groups metrics by the bot's name, the bot's alias, and by the operation, PostText\. | 

## CloudWatch Metrics for Amazon Lex Channel Associations<a name="cloudwatch-dimensions-for-aws-lex-channels"></a>

A channel association is the association between Amazon Lex and a messaging channel, such as Facebook\. The following table describes the Amazon Lex channel association metrics\.


| Metric | Description | 
| --- | --- | 
| BotChannelAuthErrors | The number of authentication errors returned by the messaging channel in the specified time period\. An authentication error indicates that the secret token provided during channel creation is invalid or has expired\.   | 
| BotChannelConfigurationErrors | The number of configuration errors in the specified period\. A configuration error indicates that one or more configuration entries for the channel are invalid\.  | 
| BotChannelInboundThrottledEvents | The number of times that messages that were sent by the messaging channel were throttled by Amazon Lex in the specified period\.   | 
| BotChannelOutboundThrottledEvents | The number of times that outbound events from Amazon Lex to the messaging channel were throttled in the specified time period\.  | 
| BotChannelRequestCount | The number of requests made on a channel in the specified time period\.  | 
| BotChannelResponseCardErrors | The number of times that Amazon Lex could not post response cards in the specified period\.  | 
| BotChannelSystemErrors | The number of internal errors that occurred in Amazon Lex for a channel in the specified period\.  | 

Amazon Lex channel association metrics use the `AWS/Lex` namespace, and provide metrics for the following dimension\. You can group metrics by dimensions in the CloudWatch console:


| Dimension | Description | 
| --- | --- | 
| BotAlias, BotChannelName, BotName, Source | Group metrics by the bot's alias, the channel name, the bot's name, and the source of traffic\. | 

## CloudWatch Metrics for Conversation Logs<a name="cloudwatch-metrics-for-logging"></a>

Amazon Lex uses the following metrics for conversation logging:


| Metric | Description | 
| --- | --- | 
| ConversationLogsAudioDeliverySuccess | The number of audio logs successfully delivered to the S3 bucket in the specified time period\. Units: Count | 
| ConversationLogsAudioDeliveryFailure | The number of audio logs that failed to be delivered to the S3 bucket in the specified time period\. A delivery failure indicates an error with the resources configured for conversation logs\. Errors can include insufficient IAM permissions, an inaccessible AWS KMS key, or an inaccessible S3 bucket\.Units: Count | 
| ConversationLogsTextDeliverySuccess | The number of text logs successfully delivered to CloudWatch Logs in the specified time period\. Units: Count | 
| ConversationLogsTextDeliveryFailure | The number of text logs that failed to be delivered to CloudWatch Logs in the specified time period\. A delivery failure indicates an error with the resources configured for conversation logs\. Errors can include insufficient IAM permissions, an inaccessible AWS KMS key, or an inaccessible CloudWatch Logs log group\. Units: Count | 

Amazon Lex conversation log metrics use the `AWS/Lex` namespace, and provide metrics for the following dimensions\. You can group metrics by dimension in the CloudWatch console\.


| Dimension | Description | 
| --- | --- | 
| `BotAlias` | Group metrics by the bot's alias\. | 
| `BotName` | Group metrics by the bot's name\. | 
| `BotVersion` | Group metrics by the bot's version\. | 