# Step 3: Add a Custom and Built\-in Intent<a name="agent-step-3"></a>

An *intent* represents an action that the call center agent wants the bot to perform\. In this case, the agent wants the bot to suggest responses and helpful resources based on the agent's conversation with the customer\. 

Amazon Lex has two types of intents: custom intents and built\-in intents\. `AMAZON.KendraSearchIntent` is a built\-in intent\. The bot uses the `AMAZON.KendraSearchIntent` intent to query the index and display the responses suggested by Amazon Kendra\. 

The bot in this example doesn't need a custom intent\. However, to build the bot, you must create at least one custom intent with at least one sample utterance\. This intent is required only to build your agent assistant bot\. It doesn’t perform any other function\. The utterance for the intent must not answer any of the questions that the customer might ask\. This ensures that the `AMAZON.KendraSearchIntent` is called to answer customer queries\. For more information, see [AMAZON\.KendraSearchIntent](lex/latest/dg/faq-bot-kendra-search.html) in the *Amazon Lex Developer Guide*\.

**To create the required custom intent**

1. On the **Getting started with your bot** page, choose **Create intent**\.

1. For **Add intent**, choose **Create intent**\.

1. In the **Create intent** dialog box, enter a descriptive name for the intent, such as **RequiredIntent**\.

1. For **Sample utterances**, enter a descriptive utterance, such as **Required utterance**\.

1. Choose **Save intent**\.

**To add the AMAZON\.KendraSearchIntent intent and response message**

1. In the navigation pane, choose the plus sign \(\+\) next to **Intents**\.

1. Choose **Search existing intents**\.

1. In the **Search intents** box, enter **AMAZON\.KendraSearchIntent**, then choose it from the list\.

1. Give the intent a descriptive name, such as **AgentAssistSearchIntent**, then choose **Add**\.

1. In the intent editor, choose **Amazon Kendra query** to open the query options\.

1. Choose the index that you want the intent to search,

1. In the **Response** section, add the following three messages to a message group\.

   ```
   I found an answer for the customer query: ((x-amz-lex:kendra-search-response-question_answer-question-1)) and the answer is ((x-amz-lex:kendra-search-response-question_answer-answer-1)).
   I found an excerpt from a helpful document: ((x-amz-lex:kendra-search-response-document-1)).
   I think this answer will help the customer: ((x-amz-lex:kendra-search-response-answer-1)).
   ```

1. Choose **Save intent**\. 

1. Choose **Build** to build the bot\.

## Next step<a name="agent-step-3-next"></a>

[Step 4: Set up Amazon Cognito](agent-step-4.md)