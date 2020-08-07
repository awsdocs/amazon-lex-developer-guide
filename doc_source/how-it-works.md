# Amazon Lex: How It Works<a name="how-it-works"></a>

Amazon Lex enables you to build applications using a speech or text interface powered by the same technology that powers Amazon Alexa\. Following are the typical steps you perform when working with Amazon Lex:

1. Create a bot and configure it with one or more intents that you want to support\. Configure the bot so it understands the user's goal \(intent\), engages in conversation with the user to elicit information, and fulfills the user's intent\.

1. Test the bot\. You can use the test window client provided by the Amazon Lex console\.

1. Publish a version and create an alias\.

1. Deploy the bot\. You can deploy the bot on platforms such as mobile applications or messaging platforms such as Facebook Messenger\. 

Before you get started, familiarize yourself with the following Amazon Lex core concepts and terminology:
+ **Bot** – A bot performs automated tasks such as ordering a pizza, booking a hotel, ordering flowers, and so on\. An Amazon Lex bot is powered by Automatic Speech Recognition \(ASR\) and Natural Language Understanding \(NLU\) capabilities, the same technology that powers Amazon Alexa\.

   

  Amazon Lex bots can understand user input provided with text or speech and converse in natural language\. You can create Lambda functions and add them as code hooks in your intent configuration to perform user data validation and fulfillment tasks\. 

   
+ **Intent** – An intent represents an action that the user wants to perform\. You create a bot to support one or more related intents\. For example, you might create a bot that orders pizza and drinks\. For each intent, you provide the following required information: 

   
  + **Intent name**– A descriptive name for the intent\. For example, **OrderPizza**\.
  + **Sample utterances** – How a user might convey the intent\. For example, a user might say "Can I order a pizza please" or "I want to order a pizza"\. 
  + **How to fulfill the intent** – How you want to fulfill the intent after the user provides the necessary information \(for example, place order with a local pizza shop\)\. We recommend that you create a Lambda function to fulfill the intent\.

     

     You can optionally configure the intent so Amazon Lex simply returns the information back to the client application to do the necessary fulfillment\. 

     

  In addition to custom intents such as ordering a pizza, Amazon Lex also provides built\-in intents to quickly set up your bot\. For more information, see [Built\-in Intents and Slot Types](howitworks-builtins.md)\. 

   
+ **Slot** – An intent can require zero or more slots or parameters\. You add slots as part of the intent configuration\. At runtime, Amazon Lex prompts the user for specific slot values\. The user must provide values for all *required* slots before Amazon Lex can fulfill the intent\.

   

  For example, the `OrderPizza` intent requires slots such as pizza size, crust type, and number of pizzas\. In the intent configuration, you add these slots\. For each slot, you provide slot type and a prompt for Amazon Lex to send to the client to elicit data from the user\. A user can reply with a slot value that includes additional words, such as "large pizza please" or "let's stick with small\." Amazon Lex can still understand the intended slot value\. 

   
+ **Slot type** – Each slot has a type\. You can create your custom slot types or use built\-in slot types\. For example, you might create and use the following slot types for the `OrderPizza` intent:

   
  + Size – With enumeration values `Small`, `Medium`, and `Large`\.
  + Crust – With enumeration values `Thick` and `Thin`\.

   

  Amazon Lex also provides built\-in slot types\. For example, `AMAZON.NUMBER` is a built\-in slot type that you can use for the number of pizzas ordered\. For more information, see [Built\-in Intents and Slot Types](howitworks-builtins.md)\.

For a list of AWS Regions where Amazon Lex is available, see [AWS Regions and Endpoints](https://docs.aws.amazon.com/general/latest/gr/rande.html#lex_region) in the *Amazon Web Services General Reference*\.

Currently, Amazon Lex supports only US English language\. That is, Amazon Lex trains your bots to understand only US English\.

The following topics provide additional information\. We recommend that you review them in order and then explore the [Getting Started with Amazon Lex](getting-started.md) exercises\.

**Topics**
+ [Programming Model](programming-model.md)
+ [Managing Messages](howitworks-manage-prompts.md)
+ [Managing Conversation Context](context-mgmt.md)
+ [Using Confidence Scores](confidence-scores.md)
+ [Conversation Logs](conversation-logs.md)
+ [Managing Sessions With the Amazon Lex API](how-session-api.md)
+ [Bot Deployment Options](chatbot-service.md)
+ [Built\-in Intents and Slot Types](howitworks-builtins.md)
+ [Custom Slot Types](howitworks-custom-slots.md)
+ [Slot Obfuscation](how-obfuscate.md)
+ [Sentiment Analysis](sentiment-analysis.md)
+ [Tagging Your Amazon Lex Resources](how-it-works-tags.md)