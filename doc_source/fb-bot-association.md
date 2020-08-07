# Integrating an Amazon Lex Bot with Facebook Messenger<a name="fb-bot-association"></a>

This exercise shows how to integrate Facebook Messenger with your Amazon Lex bot\. You perform the following steps:

1. Create an Amazon Lex bot

1. Create a Facebook application

1. Integrate Facebook Messenger with your Amazon Lex bot

1. Validate the integration

**Topics**
+ [Step 1: Create an Amazon Lex Bot](#fb-bot-assoc-create-bot)
+ [Step 2: Create a Facebook Application](#fb-bot-assoc-create-fb-app)
+ [Step 3: Integrate Facebook Messenger with the Amazon Lex Bot](#fb-bot-assoc-create-assoc)
+ [Step 4: Test the Integration](#fb-bot-test)

## Step 1: Create an Amazon Lex Bot<a name="fb-bot-assoc-create-bot"></a>

If you don't already have an Amazon Lex bot, create and deploy one\. In this topic, we assume that you are using the bot that you created in Getting Started Exercise 1\. However, you can use any of the example bots provided in this guide\. For Getting Started Exercise 1, see [Exercise 1: Create an Amazon Lex Bot Using a Blueprint \(Console\)](gs-bp.md)\.

1. Create an Amazon Lex bot\. For instructions, see [Exercise 1: Create an Amazon Lex Bot Using a Blueprint \(Console\)](gs-bp.md)\. 

1. Deploy the bot and create an alias\. For instructions, see [Exercise 3: Publish a Version and Create an Alias](gettingstarted-ex3.md)\.

## Step 2: Create a Facebook Application<a name="fb-bot-assoc-create-fb-app"></a>

On the Facebook developer portal, create a Facebook application and a Facebook page\. For instructions, see [Quick Start](https://developers.facebook.com/docs/messenger-platform/guides/quick-start) in the Facebook Messenger platform documentation\. Write down the following:
+ The **App Secret** for the Facebook App 
+ The **Page Access Token** for the Facebook page

## Step 3: Integrate Facebook Messenger with the Amazon Lex Bot<a name="fb-bot-assoc-create-assoc"></a>

In this section, you integrate Facebook Messenger with your Amazon Lex bot\.

After you complete this step, the console provides a callback URL\. Write down this URL\.

**To integrate Facebook Messenger with your bot**

1. 

   1. Sign in to the AWS Management Console and open the Amazon Lex console at [https://console\.aws\.amazon\.com/lex/](https://console.aws.amazon.com/lex/)\.

   1. Choose your Amazon Lex bot\. 

   1. Choose **Channels**\.

   1. Choose **Facebook** under **Chatbots**\. The console displays the Facebook integration page\.

   1. On the Facebook integration page, do the following:
      + Type the following name: `BotFacebookAssociation`\.
      + For **KMS key**, choose **aws/lex** \.
      + For **Alias**, choose the bot alias\.
      + For **Verify token**, type a token\. This can be any string you choose \(for example, `ExampleToken`\)\. You use this token later in the Facebook developer portal when you set up the webhook\.
      + For **Page access token**, type the token that you obtained from Facebook in Step 2\.
      + For **App secret key**, type the key that you obtained from Facebook in Step 2\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lex/latest/dg/images/fb-10a.png)

   1. Choose **Activate**\. 

      The console creates the bot channel association and returns a callback URL\. Write down this URL\.

1. On the Facebook developer portal, choose your app\.

1.  Choose the **Messenger** product, and choose **Setup webhooks** in the **Webhooks** section of the page\.

   For instructions, see [Quick Start](https://developers.facebook.com/docs/messenger-platform/guides/quick-start) in the Facebook Messenger platform documentation\. 

1. On the **webhook** page of the subscription wizard, do the following:
   + For **Callback URL**, type the callback URL provided in the Amazon Lex console earlier in the procedure\.
   + For **Verify Token**, type the same token that you used in Amazon Lex\.
   + Choose **Subscription Fields** \(**messages**, **messaging\_postbacks**, and **messaging\_optins**\)\.
   + Choose **Verify and Save**\. This initiates a handshake between Facebook and Amazon Lex\.

1. Enable Webhooks integration\. Choose the page that you created, and then choose **subscribe**\.
**Note**  
If you update or recreate a webhook, unsubscribe and then resubscribe to the page\.

## Step 4: Test the Integration<a name="fb-bot-test"></a>

You can now start a conversation from Facebook Messenger with your Amazon Lex bot\. 

1. Open your Facebook page, and choose **Message**\. 

1. In the Messenger window, use the same test utterances provided in [Step 1: Create an Amazon Lex Bot \(Console\)](gs-bp-create-bot.md)\.