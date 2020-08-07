# Example: Creating a FAQ Bot for an Amazon Kendra Index<a name="faq-bot-kendra-search"></a>

This example creates an Amazon Lex bot that uses an Amazon Kendra index to provide answers to users' questions\. The FAQ bot manages the dialog for the user\. It uses the `AMAZON.KendraSearchIntent` intent to query the index and to present the response to the user\. To create the bot, you: 

1. Create a bot that your customers will interact with to get answers from your bot\.

1. Create a custom intent\. Your bot requires at least one intent with at least one utterance\. This intent enables your bot to build, but is not used otherwise\.

1. Add the `KendraSearchIntent` intent to your bot and configure it to work with your Amazon Kendra index\.

1. Test the bot by asking questions that are answered by documents stored in your Amazon Kendra index\.

Before you can use this example, you need to create an Amazon Kendra index\. For more information, see [Getting started with an S3 bucket \(console\) ](https://docs.aws.amazon.com/kendra/latest/dg/gs-console.html) in the *Amazon Kendra Developer Guide*\.

**To create a FAQ bot**

1. Sign in to the AWS Management Console and open the Amazon Lex console at [https://console\.aws\.amazon\.com/lex/](https://console.aws.amazon.com/lex/)\.

1. In the navigation pane, choose **Bots**\. 

1. Choose **Create**\.

1. Choose **Custom bot**\. Configure the bot as follows:
   + **Bot name** – Give the bot a name that indicates its purpose, such as **KendraTestBot**\.
   + **Output voice** – Choose **None**\.
   + **Session timeout** – Enter **5**\.
   + **Sentiment analysis** – Choose **No**\.
   + **COPPA** – Choose **No**\.
   + **User utterance storage** – Choose **Do not store**\.

1. Choose **Create**\.

To successfully build a bot, you must create at least one intent with at least one sample utterance\. This intent is required to build your Amazon Lex bot, but isn't used for the FAQ response\. The utterance for the intent must not apply to any of the questions that your customer asks\.

**To create the required intent**

1. On the **Getting started with your bot** page, choose **Create intent**\.

1. For **Add intent**, choose **Create intent**\.

1. In the **Create intent** dialog box, give the intent a name, such as **RequiredIntent**\.

1. For **Sample utterances**, type an utterance, such as **Required utterance**\.

1. Choose **Save intent**\.

Now, create the intent to search an Amazon Kendra index and the response messages that it should return\.

**To create an AMAZON\.KendraSearchIntent intent and response message**

1. In the navigation pane, choose the plus \(\+\) next to **Intents**\.

1. For **Add intent**, choose **Search existing intents**\.

1. In the **Search intents**box, enter **AMAZON\.KendraSearchIntent**, then choose it from the list\.

1. For **Copy built\-in intent**, give the intent a name, such as **KendraSearchIntent**, and then choose **Add**\. 

1. In the intent editor, choose **Amazon Kendra query** to open the query options\.

1. From the **Amazon Kendra index** menu, choose the index that you want the intent to search\.

1. In the **Response** section, add the following three messages:

   ```
   I found a FAQ question for you: ((x-amz-lex:kendra-search-response-question_answer-question-1)) and the answer is ((x-amz-lex:kendra-search-response-question_answer-answer-1)).
   I found an excerpt from a helpful document: ((x-amz-lex:kendra-search-response-document-1)).
   I think the answer to your questions is ((x-amz-lex:kendra-search-response-answer-1)).
   ```

1. Choose **Save intent**, and then choose **Build** to build the bot\.

Finally, use the console test window to test responses from your bot\. Your questions should be in the domain that your index supports\.

**To test your FAQ bot**

1. In the console test window, type a question for your index\.

1. Verify the answer in the test window's response section\.

1. To reset the test window for another question, choose **Clear chat history**\.