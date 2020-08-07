# Integrating an Amazon Lex Bot with Twilio Programmable SMS<a name="twilio-bot-association"></a>

This exercise provides instructions for integrating an Amazon Lex bot with the Twilio simple messaging service \(SMS\)\. You perform the following steps:

1. Create an Amazon Lex bot

1. Integrate Twilio programmable SMS with your bot Amazon Lex

1. Engage in an interaction with the Amazon Lex bot by testing the setup using the SMS service on your mobile phone

1. Test the integration 

**Topics**
+ [Step 1: Create an Amazon Lex Bot](#twilio-bot-assoc-create-bot)
+ [Step 2: Create a Twilio SMS Account](#twilio-bot-assoc-create-fb-app)
+ [Step 3: Integrate the Twilio Messaging Service Endpoint with the Amazon Lex Bot](#twilio-bot-assoc-create-assoc)
+ [Step 4: Test the Integration](#twilio-bot-test)

## Step 1: Create an Amazon Lex Bot<a name="twilio-bot-assoc-create-bot"></a>

If you don't already have an Amazon Lex bot, create and deploy one\. In this topic, we assume that you are using the bot that you created in Getting Started Exercise 1\. However, you can use any of the example bots provided in this guide\. For Getting Started Exercise 1, see [Exercise 1: Create an Amazon Lex Bot Using a Blueprint \(Console\)](gs-bp.md)\.

1. Create an Amazon Lex bot\. For instructions, see [Exercise 1: Create an Amazon Lex Bot Using a Blueprint \(Console\)](gs-bp.md)\. 

1. Deploy the bot and create an alias\. For instructions, see [Exercise 3: Publish a Version and Create an Alias](gettingstarted-ex3.md)\.

## Step 2: Create a Twilio SMS Account<a name="twilio-bot-assoc-create-fb-app"></a>

Sign up for a Twilio account and record the following account information: 
+ **ACCOUNT SID** 
+ **AUTH TOKEN** 

For sign\-up instructions, see [https://www\.twilio\.com/console](https://www.twilio.com/console)\.

## Step 3: Integrate the Twilio Messaging Service Endpoint with the Amazon Lex Bot<a name="twilio-bot-assoc-create-assoc"></a>

**To integrate Twilio with your Amazon Lex bot**

1. To associate the Amazon Lex bot with your Twilio programmable SMS endpoint, activate bot channel association in the Amazon Lex console\. When the bot channel association has been activated, Amazon Lex returns a callback URL\. Record this callback URL because you need it later\.

   1. Sign in to the AWS Management Console and open the Amazon Lex console at [https://console\.aws\.amazon\.com/lex/](https://console.aws.amazon.com/lex/)\.

   1. Choose the Amazon Lex bot that you created in Step 1\.

   1. Choose the **Channels** tab\.

   1. In the **Chatbots** section, choose **Twilio SMS**\. 

   1. On the **Twilio SMS** page, provide the following information:
      + Type a name\. For example, `BotTwilioAssociation`\.
      + Choose "aws/lex" from **KMS key**\.
      + For **Alias**, choose the bot alias\.
      + For **Authentication Token**, type the AUTH TOKEN for your Twilio account\. 
      + For **Account SID**, type the ACCOUNT SID for your Twilio account\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lex/latest/dg/images/twilio-10a.png)

   1. Choose **Activate**\. 

      The console creates the bot channel association and returns a callback URL\. Record this URL\.

1. On the Twilio console, connect the Twilio SMS endpoint to the Amazon Lex bot\.

   1. Sign in to the Twilio console at [https://www\.twilio\.com/console](https://www.twilio.com/console)\. 

   1. If you don't have a Twilio SMS endpoint, create it\.

   1. Update the **Inbound Settings** configuration of the messaging service by setting the **REQUEST URL** value to the callback URL that Amazon Lex provided in the preceding step\.

## Step 4: Test the Integration<a name="twilio-bot-test"></a>

Use your mobile phone to test the integration between Twilio SMS and your bot\.

**To test integration**

1. Sign in to the Twilio console at [https://www\.twilio\.com/console](https://www.twilio.com/console) and do the following:

   1. Verify that you have a Twilio number associated with the messaging service under **Manage Numbers**\. 

      You send messages to this number and engage in SMS interaction with the Amazon Lex bot from your mobile phone\. 

   1. Verify that your mobile phone is listed as **Verified Caller ID**\. 

      If it isn't, follow instructions on the Twilio console to enable the mobile phone that you plan to use for testing\. 

      Now you can use your mobile phone to send messages to the Twilio SMS endpoint, which is mapped to the Amazon Lex bot\. 

1. Using your mobile phone, send messages to the Twilio number\. 

   The Amazon Lex bot responds\. If you created the bot using Getting Started Exercise 1, you can use the example conversations provided in that exercise\. For more information, see [Step 4: Add the Lambda Function as Code Hook \(Console\)](gs-bp-create-integrate.md)\.