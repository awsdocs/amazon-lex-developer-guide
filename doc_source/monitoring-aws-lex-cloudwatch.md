# Monitoring Amazon Lex with Amazon CloudWatch<a name="monitoring-aws-lex-cloudwatch"></a>

 To track the health of your Amazon Lex bots, use Amazon CloudWatch\. With CloudWatch, you can get metrics for individual Amazon Lex operations or for global Amazon Lex operations for your account\. \. You can also set up CloudWatch alarms to be notified when one or more metrics exceeds a threshold that you define\. For example, you can monitor the number of requests made to a bot over a particular time period, view the latency of successful requests, or raise an alarm when errors exceed a threshold\.

## CloudWatch Metrics for Amazon Lex<a name="aws-lex-cloudwatch-using"></a>

To get metrics for your Amazon Lex operations , you must specify the following information:

+ The metric dimension\. A *dimension* is a set of name\-value pairs that you use to identify a metric\. Amazon Lex has three dimensions: 

  + `BotAlias, BotName, Operation`

  + `BotAlias, BotName, InputMode, Operation`

  + `BotName, BotVersion, InputMode, Operation`

+ The metric name, such as `MissedUtteranceCount` or `RuntimeRequestCount`\.

You can get metrics for Amazon Lex with the AWS Management Console, the AWS CLI, or the CloudWatch API\. You can use the CloudWatch API through one of the Amazon AWS Software Development Kits \(SDKs\) or the CloudWatch API tools\. The Amazon Lex console displays graphs based on the raw data from the CloudWatch API\. 

You must have the appropriate CloudWatch permissions to monitor Amazon Lex with CloudWatch For more information, see [ Authentication and Access Control for Amazon CloudWatch](http://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/auth-and-access-control-cw.html) in the *Amazon CloudWatch User Guide*\.

## Viewing Amazon Lex Metrics<a name="aws-lex-cloudwatch-metrics"></a>

View Amazon Lex metrics using the Amazon Lex console and the CloudWatch console\.

**To view metrics \(Amazon Lex console\)**

1. Sign in to the AWS Management Console and open the Amazon Lex console at [https://console\.aws\.amazon\.com/lex/](https://console.aws.amazon.com/lex/)\.

1. From the list of bots, choose the one whose metrics you want to see\.

1. Choose **Monitoring**\. Metrics are displayed in graphs\.

**To view metrics \(CloudWatch console\)**

1. Sign in to the AWS Management Console and open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. Choose **Metrics**, choose **All Metrics**, and then choose **AWS/Lex**\.

1. Choose the dimension, and then choose a metric name\. Choose **Add to graph**\.

1. Choose a value for the date range\. The metric count for the selected date range is displayed in the graph\.

## Creating an Alarm<a name="aws-lex-cloudwatch-alarms"></a>

A CloudWatch alarm watches a single metric over a time period that you specify, and performs one or more actions: sending a notification to an Amazon SNS topic or Auto Scaling policy\. The action or actions are based on the value of the metric relative to a given threshold over a number of time periods that you specify\. CloudWatch can also send you an Amazon Simple Notification Service \(Amazon SNS\) message when the alarm changes state\. \. \.

CloudWatch alarms invoke actions only when the state changes and has persisted for the period that you specify\.

**To set an alarm**

1. Sign in to the AWS Management Console and open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. Choose **Alarms**, and then choose **Create Alarm**\. 

1. Choose **AWS/Lex Metrics**, and then choose a metric\.

1. For **Time Range**, choose a time range to monitor, and then choose **Next**\.

1. Type a **Name** and **Description**\.

1.  For **Whenever**, choose **>=**, and type a maximum value\.

1. If you want CloudWatch to send an email when the alarm state is reached, in the **Actions** section, for **Whenever this alarm**, choose **State is ALARM**\. For **Send notification to**, choose a mailing list or choose **New list** and create a new list\.

1. Preview the alarm in the **Alarm Preview** section\. If you are satisfied with the alarm, choose **Create Alarm**\.