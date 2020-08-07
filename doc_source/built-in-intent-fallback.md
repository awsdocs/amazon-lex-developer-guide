# AMAZON\.FallbackIntent<a name="built-in-intent-fallback"></a>

When a user's input to an intent isn't what a bot expects, you can configure Amazon Lex to invoke a *fallback intent*\. For example, if the user input "I'd like to order candy" doesn't match an intent in your `OrderFlowers` bot, Amazon Lex invokes the fallback intent to handle the response\.

You add a fallback intent by adding the built\-in `AMAZON.FallbackIntent` intent type to your bot\. You can specify the intent using the [PutBot](API_PutBot.md) operation or by choosing the intent from the list of built\-in intents in the console\. 

Invoking a fallback intent uses two steps\. In the first step the fallback intent is matched based on the input from the user\. When the fallback intent is matched, the way the bot behaves depends on the number of retries configured for a prompt\. For example, if the maximum number of attempts to determine an intent is 2, the bot returns the bot's clarification prompt twice before invoking the fallback intent\.

Amazon Lex matches the fallback intent in these situations: 
+ The user's input to an intent doesn't match the input that the bot expects
+ Audio input is noise, or text input isn't recognized as words\.
+ The user's input is ambiguous and Amazon Lex can't determine which intent to invoke\.

The fallback intent is invoked when:
+ The bot doesn't recognize the user input as an intent after the configured number of tries for clarification when the conversation is started\.
+ An intent doesn't recognize the user input as a slot value after the configured number of tries\.
+ An intent doesn't recognize the user input as a response to a confirmation prompt after the configured number of tries\.

You can use the following with a fallback intent:
+ A fulfillment Lambda function
+ A conclusion statement
+ A follow up prompt

You can't add the following to a fallback intent:
+ Utterances
+ Slots
+ An initialization and validation Lambda function 
+ A confirmation prompt

If you have configured both a cancel statement and a fallback intent for a bot, Amazon Lex uses the fallback intent\. If you need your bot to have a cancel statement, you can use the fulfillment function for the fallback intent to provide the same behavior as a cancel statement\. For more information, see the `abortStatement` parameter of the [PutBot](API_PutBot.md) operation\.

## Using Clarification Prompts<a name="fallback-clarification"></a>

If you provide your bot with a clarification prompt, the prompt is used to solicit a valid intent from the user\. The clarification prompt will be repeated the number of times that you configured\. After that the fallback intent will be invoked\.

If you don't set a clarification prompt when you create a bot and the user doesn't start the conversation with a valid intent, Amazon Lex immediately calls your fallback intent \. 

When you use a fallback intent without a clarification prompt, Amazon Lex doesn't call the fallback under these circumstances:
+ When the user responds to a follow\-up prompt but doesn't provide an intent\. For example, in response to a follow\-up prompt that says "Would you like anything else today?", the user says "Yes\." Amazon Lex returns a 400 Bad Request exception because it doesn't have a clarification prompt to send to the user to get an intent\.
+ When using an AWS Lambda function, you return an `ElicitIntent` dialog type\. Because Amazon Lex doesn't have a clarification prompt to get an intent from the user, it returns a 400 Bad Request exception\.
+ When using the `PutSession` operation, you send an `ElicitIntent` dialog type\. Because Amazon Lex doesn't have a clarification prompt to get an intent from the user, it returns a 400 Bad Request exception\.

## Using a Lambda Function with a Fallback Intent<a name="invoke-fallback"></a>

When a fallback intent is invoked, the response depends on the setting of the `fulfillmentActivity` parameter to the [PutIntent](API_PutIntent.md) operation\. The bot does one of the following:
+ Returns the intent information to the client application\.
+ Calls the fulfillment Lambda function\. It calls the function with the session variables that are set for the session\.

For more information about setting the response when a fallback intent is invoked, see the `fulfillmentActivity` parameter of the [PutIntent](API_PutIntent.md) operation\. 

If you use the fulfillment Lambda function in your fallback intent, you can use this function to call another intent or to perform some form of communication with the user, such as collecting a callback number or opening a session with a customer service representative\.

You can perform any action in a fallback intent Lambda function that you can perform in the fulfillment function for any other intent\. For more information about creating a fulfillment function using AWS Lambda, see [Using Lambda Functions](using-lambda.md)\.

A fallback intent can be invoked multiple times in the same session\. For example, suppose that your Lambda function uses the `ElicitIntent` dialog action to prompt the user for a different intent\. If Amazon Lex can't infer the user's intent after the configured number of tries, it invokes the fallback intent again\. It also invokes the fallback intent when the user doesn't respond with a valid slot value after the configured number of tries\.

You can configure a Lambda function to keep track of the number of times that the fallback intent is called using a session variable\. Your Lambda function can take a different action if it is called more times than the threshold that you set in your Lambda function\. For more information about session variables, see [Setting Session Attributes](context-mgmt.md#context-mgmt-session-attribs)\.