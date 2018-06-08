# Exercise 1: Create an Amazon Lex Bot Using a Blueprint \(Console\)<a name="gs-bp"></a>

In this exercise, you do the following:
+ Create your first Amazon Lex bot, and test it in the Amazon Lex console\. 

  For this exercise, you use the **OrderFlowers** blueprint\. For information about blueprints, see [Amazon Lex and AWS Lambda Blueprints](lex-lambda-blueprints.md)\. 

   
+ Create an AWS Lambda function and test it in the Lambda console\. While processing a request, your bot calls this Lambda function\. For this exercise, you use a Lambda blueprint \(**lex\-order\-flowers\-python**\) provided in the AWS Lambda console to create your Lambda function\. The blueprint code illustrates how you can use the same Lambda function to perform initialization and validation, and to fulfill the `OrderFlowers` intent\. 

   
+ Update the bot to add the Lambda function as the code hook to fulfill the intent\. Test the end\-to\-end experience\.

The following sections explain what the blueprints do\. 

## Amazon Lex Bot: Blueprint Overview<a name="gs-bp-summary-bot"></a>

You use the **OrderFlowers** blueprint to create an Amazon Lex bot\.For more information about the structure of a bot, see [Amazon Lex: How It Works](how-it-works.md)\. The bot is preconfigured as follows:
+ **Intent** – OrderFlowers
+ **Slot types** – One custom slot type called `FlowerTypes` with enumeration values: `roses`, `lilies`, and `tulips`\.
+ **Slots** – The intent requires the following information \(that is, slots\) before the bot can fulfill the intent\.
  + `PickupTime` \(AMAZON\.TIME built\-in type\)
  + `FlowerType` \(FlowerTypes custom type\)
  + `PickupDate` \(AMAZON\.DATE built\-in type\)
+ **Utterance** – The following sample utterances indicate the user's intent:
  + "I would like to pick up flowers\."
  + "I would like to order some flowers\."
+ **Prompts** – After the bot identifies the intent, it uses the following prompts to fill the slots:
  + Prompt for the `FlowerType` slot – "What type of flowers would you like to order?"
  + Prompt for the `PickupDate` slot – "What day do you want the \{FlowerType\} to be picked up?"
  + Prompt for the `PickupTime` slot – "At what time do you want the \{FlowerType\} to be picked up?"
  + Confirmation statement – "Okay, your \{FlowerType\} will be ready for pickup by \{PickupTime\} on \{PickupDate\}\. Does this sound okay?" 

## AWS Lambda Function: Blueprint Summary<a name="gs-bp-summary-lambda"></a>

The Lambda function in this exercise performs both initialization and validation and fulfillment tasks\. Therefore, after creating the Lambda function, you update the intent configuration by specifying the same Lambda function as a code hook to handle both the initialization and validation and fulfillment tasks\. 
+ As an initialization and validation code hook, the Lambda function performs basic validation\. For example, if the user provides a time for pickup that is outside of normal business hours, the Lambda function directs Amazon Lex to re\-prompt the user for the time\.
+ As part of the fulfillment code hook, the Lambda function returns a summary message indicating that the flower order has been placed \(that is, the intent is fulfilled\)\.

**Next Step**  
[Step 1: Create an Amazon Lex Bot \(Console\)](gs-bp-create-bot.md)