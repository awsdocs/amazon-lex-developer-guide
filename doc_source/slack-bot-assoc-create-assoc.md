# Step 4: Integrate the Slack Application with the Amazon Lex Bot<a name="slack-bot-assoc-create-assoc"></a>

Now that you have Slack application credentials, you can integrate the application with your Amazon Lex bot\. To associate the Slack application with your bot, add a bot channel association in Amazon Lex\.

In the Amazon Lex console, activate a bot channel association to associate the bot with your Slack application\. When the bot channel association is activated, Amazon Lex returns two URLs \(**Postback URL** and **OAuth URL**\)\. Record these URLs because you need them later\.

**To integrate the Slack application with your Amazon Lex bot**

1. Sign in to the AWS Management Console, and open the Amazon Lex console at [https://console\.aws\.amazon\.com/lex/](https://console.aws.amazon.com/lex/)\. 

1. Choose the Amazon Lex bot that you created in Step 1\.

1. Choose the **Channels** tab\.

1. In the left menu, choose **Slack**\. 

1. On the **Slack** page, provide the following:
   + Type a name\. For example, `BotSlackIntegration`\.
   + Choose "aws/lex" from the **KMS key** drop\-down\.
   + For **Alias**, choose the bot alias\.
   + Type the **Client Id**, **Client secret**, and **Verification Token**, which you recorded in the preceding step\. These are the credentials of the Slack application\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lex/latest/dg/images/slack-10a.png)

1. Choose **Activate**\. 

   The console creates the bot channel association and returns two URLs \(Postback URL and OAuth URL\)\. Record them\. In the next section, you update your Slack application configuration to use these endpoints as follows:
   + The Postback URL is the Amazon Lex bot's endpoint that listens to Slack events\. You use this URL: 
     + As the request URL in the **Event Subscriptions** feature of the Slack application\.
     + To replace the placeholder value for the request URL in the **Interactive Messages** feature of the Slack application\.
   + The OAuth URL is your Amazon Lex bot's endpoint for an OAuth handshake with Slack\. 

**Next Step**  
[Step 5: Complete Slack Integration](slack-bot-back-in-slack-console.md)