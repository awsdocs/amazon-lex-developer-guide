# Step 2: Create an Amazon Lex Bot<a name="agent-step-2"></a>

Amazon Lex provides an interface between the call center agent and the Amazon Kendra index\. It keeps track of the conversation between the agent and the customer and calls the `AMAZON.KendraSearchIntent` intent based on the questions the customer asks\. An *intent* is an action that the user wants to perform\.

Amazon Kendra searches the indexed documents and returns an answer to Amazon Lex that it displays in the bot\. This answer is visible only to the agent\.

**To create an agent assistant bot**

1. Sign in to the AWS Management Console and open the Amazon Lex console at [https://console\.aws\.amazon\.com/lex/](https://console.aws.amazon.com/lex/)\.

1. In the navigation pane, choose **Bots**\.

1. Choose **Create**\.

1. Choose **Custom bot** and configure the bot\.

   1. **Bot name** – Enter a name that indicates the bot's purpose, such as **AgentAssistBot**\.

   1. **Output voice** – Choose **None**\.

   1. **Session timeout** – Enter **5**\.

   1. **COPPA** – Choose **No**\.

1. Choose **Create**\. After creating the bot, Amazon Lex displays the bot editor tab\.

## Next step<a name="agent-step-2-next"></a>

[Step 3: Add a Custom and Built\-in Intent](agent-step-3.md)