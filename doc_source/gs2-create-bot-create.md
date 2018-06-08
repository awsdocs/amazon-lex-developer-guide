# Create the Bot<a name="gs2-create-bot-create"></a>

Create the `PizzaOrderingBot` bot with the minimum information needed\. You add an intent, an action that the user wants to perform, for the bot later\.

**To create the bot**

1. Sign in to the AWS Management Console and open the Amazon Lex console at [https://console\.aws\.amazon\.com/lex/](https://console.aws.amazon.com/lex/)\.

1. Create a bot\.

   1. If you are creating your first bot, choose **Get Started**\. Otherwise, choose **Bots**, and then choose **Create**\. 

   1. On the **Create your Lex bot** page, choose **Custom bot** and provide the following information:
      + **App name**: PizzaOrderingBot 
      + **Output voice**: Salli 
      + **Session timeout **: 5 minutes\.
      + **Child\-Directed**: Choose the appropriate response\.

   1. Choose **Create**\. 

      The console sends Amazon Lex a request to create a new bot\. Amazon Lex sets the bot version to `$LATEST`\. After creating the bot, Amazon Lex shows the bot **Editor** tab:  
![\[\]](http://docs.aws.amazon.com/lex/latest/dg/images/gs1-20.png)
      + The bot version, **Latest**, appears next to the bot name in the console\. New Amazon Lex resources have `$LATEST` as the version\. For more information, see [Versioning and Aliases](versioning-aliases.md)\.
      + Because you haven't created any intents or slots types, none are listed\. 
      + **Build** and **Publish** are bot\-level activities\. After you configure the entire bot, you'll learn more about these activities\.

## Next Step<a name="gs2-next-step-intent"></a>

[Create an Intent](gs2-create-bot-intent.md)