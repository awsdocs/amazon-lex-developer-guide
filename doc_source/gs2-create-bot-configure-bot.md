# Configure the Bot<a name="gs2-create-bot-configure-bot"></a>

Configure error handling for the `PizzaOrderingBot` bot\.

1. Navigate to the `PizzaOrderingBot` bot\. Choose **Editor**\. and then choose **Error Handling**\.  
![\[\]](http://docs.aws.amazon.com/lex/latest/dg/images/gs1-80.png)

1. Use the **Editor** tab to configure bot error handling\.
   + Information you provide in **Clarification Prompts** maps to the bot's [clarificationPrompt](https://docs.aws.amazon.com/lex/latest/dg/API_PutBot.html#lex-PutBot-request-clarificationPrompt) configuration\. 

     When Amazon Lex can't determine the user intent, the service returns a response with this message\. 
   + Information that you provide in the **Hang\-up** phrase maps to the bot's [abortStatement](https://docs.aws.amazon.com/lex/latest/dg/API_PutBot.html#lex-PutBot-request-abortStatement) configuration\. 

     If the service can't determine the user's intent after a set number of consecutive requests, Amazon Lex returns a response with this message\.

   Leave the defaults\.

## Next Step<a name="gs2-next-step-build-and-test"></a>

[Step 3: Build and Test the Bot](gs2-build-and-test.md)