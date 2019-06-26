# Example: Updating Utterances<a name="ex-utterances"></a>

In this exercise, you add additional utterances to those you created in Getting Started Exercise 1\. You use the **Monitoring** tab in the Amazon Lex console to view utterances that your bot did not recognize\. To improve the experience for your users, you add those utterances to the bot\. 

**Note**  
Utterance statistics are generated once a day\. You can see the utterance that was not recognized, how many times it was heard, and the last date and time that the utterance was heard\. It can take up to 24 hours for missed utterances to appear in the console\.

You can see utterances for different versions of your bot\. To change the version of your bot that you are seeing utterances for, choose a different version from the drop\-down next to the bot name\.

**To view and add missed utterances to a bot:**

1. Follow the first step of Getting Started Exercise 1 to create and test an `OrderFlowers` bot\. For instructions, see [Exercise 1: Create an Amazon Lex Bot Using a Blueprint \(Console\)](gs-bp.md)\.

1. Test the bot by typing the following utterances in the **Test Bot** window\. Type each utterance several times\. The example bot doesn't recognize the following utterances:
   + Order flowers
   + Get me flowers
   + Please order flowers
   + Get me some flowers

1. Wait for Amazon Lex to gather usage data about the missed utterances\. Utterance data is generated once per day, generally overnight\.

1. Sign in to the AWS Management Console and open the Amazon Lex console at [https://console\.aws\.amazon\.com/lex/](https://console.aws.amazon.com/lex/)\.

1. Choose the `OrderFlowers` bot\.

1. Choose the **Monitoring** tab, and then choose **Utterances** from the left menu and then choose the **Missed** button\. The pane shows a maximum of 100 missed utterances\.  
![\[The Utterances pane showing missed utterances.\]](http://docs.aws.amazon.com/lex/latest/dg/images/utterances-10.png)

1. To choose the missed utterances that you want to add to the bot, select the check box next to them\. To add the utterance to the `$LATEST` version of the intent, choose the down arrow next to the **Add utterance to intent** dropdown, and then choose the intent\.

1. To rebuild your bot, choose **Build** and then **Build** again to re\-build your bot\.

1. To verify that your bot recognizes the new utterances, use the **Test Bot** pane\.