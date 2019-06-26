# Step 7 \(Optional\): Clean Up \(Console\)<a name="gs-bp-cleaning-up"></a>

Now, delete the resources that you created and clean up your account\.

You can delete only resources that are not in use\. In general, you should delete resources in the following order:
+ Delete bots to free up intent resources\.
+ Delete intents to free up slot type resources\.
+ Delete slot types last\.

**To clean up your account \(console\)**

1. Sign in to the AWS Management Console and open the Amazon Lex console at [https://console\.aws\.amazon\.com/lex/](https://console.aws.amazon.com/lex/)\.

1. From the list of bots, choose the check box next to **OrderFlowers**\.

1. To delete the bot, choose **Delete**, and then choose **Continue** in the confirmation dialog box\.

1. In the left pane, choose **Intents**\.

1. In the list of intents, choose **OrderFlowersIntent**\.

1. To delete the intent, choose **Delete**, and then choose **Continue** in the confirmation dialog box\.

1. In the left pane, choose **Slot types**\.

1. In the list of slot types, choose **Flowers**\.

1. To delete the slot type, choose **Delete**, and then choose **Continue** in the confirmation dialog box\.

You have removed all of the Amazon Lex resources that you created and cleaned up your account\. If desired, you can use the [Lambda console](https://console.aws.amazon.com/lambda) to delete the Lambda function used in this exercise\.