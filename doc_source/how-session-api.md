# Managing Sessions With the Amazon Lex API<a name="how-session-api"></a>

When a user starts a conversation with your bot, Amazon Lex creates a *session*\. The information exchanged between your application and Amazon Lex makes up the session state for the conversation\. When you make a request, the session is identified by a combination of the bot name and a user identifier that you specify\. For more information about the user identifier, see the `userId` field in the [PostContent](API_runtime_PostContent.md) or [PostText](API_runtime_PostText.md) operation\.

The response from a session operation includes a unique session identifier that identifies a specific session with a user\. You can use this identifier during testing or to help troubleshoot your bot\.

You can modify the session state sent between your application and your bot\. For example, you can create and modify session attributes that contain custom information about the session, and you can change the flow of the conversation by setting the dialog context to interpret the next utterance\.

There are two ways that you can update session state\. The first is to use a Lambda function with the `PostContent` or `PostText` operation that is called after each turn of the conversation\. For more information, see [Using Lambda Functions](using-lambda.md)\. The other is to use the Amazon Lex runtime API in your application to make changes to the session state\. 

The Amazon Lex runtime API provides operations that enable you to manage session information for a conversation with your bot\. The operations are the [PutSession](API_runtime_PutSession.md) operation, the [GetSession](API_runtime_GetSession.md) operation, and the [DeleteSession](API_runtime_DeleteSession.md) operation\. You use these operations to get information about the state of your user's session with your bot, and to have fine\-grained control over the state\.

Use the `GetSession` operation when you want to get the current state of the session\. The operation returns the current state of the session, including the state of the dialog with your user, any session attributes that have been set and slot values for the last three intents that the user interacted with\. 

The `PutSession` operation enables you to directly manipulate the current session state\. You can set the type of dialog action that the bot will perform next\. This gives you control over the flow of the conversation with the bot\. Set the dialog action `type` field to `Delegate` to have Amazon Lex determine the next action for the bot\.

You can use the `PutSession` operation to create a new session with a bot and set the intent that the bot should start with\. You can also use the `PutSession` operation to change from one intent to another\. When you create a session or change the intent you also can set session state, such as slot values and session attributes\. When the new intent is finished, you have the option of restarting the prior intent\. You can use the `GetSession` operation to get the dialog state of the prior intent from Amazon Lex and use the information to set the dialog state of the intent\.

The response from the `PutSession` operation contains the same information as the `PostContent` operation\. You can use this information to prompt the user for the next piece of information, just as you would with the response from the `PostContent` operation\.

Use the `DeleteSession` operation to remove an existing session and start over with a new session\. For example, when you are testing your bot you can use the `DeleteSession` operation to remove test sessions from your bot\.

The session operations work with your fulfillment Lambda functions\. For example, if your Lambda function returns `Failed` as the fulfillment state you can use the `PutSession` operation to set the dialog action type to `close` and `fulfillmentState` to `ReadyForFulfillment` to retry the fulfillment step\.

Here are some things that you can do with the session operations:
+ Have the bot start a conversation instead of waiting for the user\.
+ Switch intents during a conversation\.
+ Return to a previous intent\.
+ Start or restart a conversation in the middle of the interaction\.
+ Validate slot values and have the bot re\-prompt for values that are not valid\.

Each of these are described further below\.

## Switching Intents<a name="session-switch"></a>

You can use the `PutSession` operation to switch from one intent to another\. You can also use it to switch back to a previous intent\. You can use the `PutSession` operation to set session attributes or slot values for the new intent\.
+ Call the `PutSession` operation\. Set the intent name to the name of the new intent and set the dialog action to `Delegate`\. You can also set any slot values or session attributes required for the new intent\.
+ Amazon Lex will start a conversation with the user using the new intent\.

## Resuming a Prior Intent<a name="session-return"></a>

To resume a prior intent you use the `GetSession` operation to get the summary of the intent, and then use the `PutSession` operation to set the intent to its previous dialog state\.
+ Call the `GetSession` operation\. The response from the operation includes a summary of the dialog state of the last three intents that the user interacted with\.
+ Using the information from the intent summary, call the `PutSession` operation\. This will return the user to the previous intent in the same place in the conversation\.

In some cases it may be necessary to resume your user's conversation with your bot\. For example, say that you have created a customer service bot\. Your application determines that the user needs to talk to a customer service representative\. After talking to the user, the representative can direct the conversation back to the bot with the information that they collected\.

To resume a session, use steps similar to these:
+ Your application determines that the user needs to speak to a customer service representative\.
+ Use the `GetSession` operation to get the current dialog state of the intent\. 
+ The customer service representative talks to the user and resolves the issue\.
+ Use the `PutSession` operation to set the dialog state of the intent\. This may include setting slot values, setting session attributes, or changing the intent\.
+ The bot resumes the conversation with the user\.

You can use the `PutSession` operation `checkpointLabel` parameter to label an intent so that you can find it later\. For example, a bot that asks a customer for information might go into a `Waiting` intent while the customer gathers the information\. The bot creates a checkpoint label for the current intent and then starts the `Waiting` intent\. When the customer returns the bot can find the previous intent using the checkpoint label and switch back\. 

The intent must be present in the `recentIntentSummaryView` structure returned by the `GetSession` operation\. If you specify a checkpoint label in the `GetSession` operation request, it will return a maximum of three intents with that checkpoint label\.
+ Use the `GetSession` operation to get the current state of the session\.
+ Use the `PutSession` operation to add a checkpoint label to the last intent\. If necessary you can use this `PutSession` call to switch to a different intent\.
+ When it is time to switch back to the labeled intent, call the `GetSession` operation to return a recent intent list\. You can use the `checkpointLabelFilter` parameter so that Amazon Lex returns only intents with the specified checkpoint label\.

## Starting a New Session<a name="session-start"></a>

If you want to have the bot start the conversation with your user, you can use the `PutSession` operation\. 
+ Create a welcome intent with no slots and a conclusion message that prompts the user to state an intent\. For example, "What would you like to order? You can say 'Order a drink' or 'Order a pizza\.'"
+ Call the `PutSession` operation\. Set the intent name to the name of your welcome intent and set the dialog action to `Delegate`\. 
+ Amazon Lex will respond with the prompt from your welcome intent to start the conversation with your user\.

## Validating Slot Values<a name="session-validation"></a>

You can validate responses to your bot using your client application\. If the response isn't valid, you can use the `PutSession` operation to get a new response from your user\. For example, suppose that your flower ordering bot can only sell tulips, roses, and lilies\. If the user orders carnations, your application can do the following:
+ Examine the slot value returned from the `PostText` or `PostContent` response\.
+ If the slot value is not valid, call the `PutSession` operation\. Your application should clear the slot value, set the `slotToElicit` field, and set the `dialogAction.type` value to `elicitSlot`\. Optionally, you can set the `message` and `messageFormat` fields if you want to change the message that Amazon Lex uses to elicit the slot value\.