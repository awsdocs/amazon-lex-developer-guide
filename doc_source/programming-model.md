# Programming Model<a name="programming-model"></a>

A *bot* is the primary resource type in Amazon Lex\. The other resource types in Amazon Lex are *intent*, *slot type*, *alias*, and *bot channel association*\. 

You create a bot using the Amazon Lex console or the model building API\. The console provides a graphical user interface that you use to build a production\-ready bot for your application\. If you prefer, you can use the model building API through the AWS CLI or your own custom program to create a bot\. 

After you create a bot, you deploy it on one of the [supported platforms](https://docs.aws.amazon.com/lex/latest/dg/chatbot-service.html) or integrate it into your own application\. When a user interacts with the bot, the client application sends requests to the bot using the Amazon Lex runtime API\. For example, when a user says "I want to order pizza," your client sends this input to Amazon Lex using one of the runtime API operations\. Users can provide input as speech or text\. 

You can also create Lambda functions and use them in an intent\. Use these Lambda function code hooks to perform runtime activities such as initialization, validation of user input, and intent fulfillment\. The following sections provide additional information\.

**Topics**
+ [Model Building API Operations](#programming-model-build-time-api)
+ [Runtime API Operations](#programming-model-runtime-api)
+ [Lambda Functions As Code Hooks](#prog-model-lambda)

## Model Building API Operations<a name="programming-model-build-time-api"></a>

To programmatically create bots, intents, and slot types, use the model building API operations\. You can also use the model building API to manage, update, and delete resources for your bot\. The model building API operations include:
+ [PutBot](API_PutBot.md), [PutBotAlias](API_PutBotAlias.md), [PutIntent](API_PutIntent.md), and [PutSlotType](API_PutSlotType.md) to create and update bots, bot aliases, intents, and slot types, respectively\.
+ [CreateBotVersion](API_CreateBotVersion.md), [CreateIntentVersion](API_CreateIntentVersion.md), and [CreateSlotTypeVersion](API_CreateSlotTypeVersion.md) to create and publish versions of your bots, intents, and slot types, respectively\.
+ [GetBot](API_GetBot.md) and [GetBots](API_GetBots.md) to get a specific bot or a list of bots that you have created, respectively\.
+ [GetIntent](API_GetIntent.md) and [GetIntents](API_GetIntents.md) to get a specific intent or a list of intents that you have created, respectively\.
+ [GetSlotType](API_GetSlotType.md) and [GetSlotTypes](API_GetSlotTypes.md) to get a specific slot type or a list of slot types that you have created, respectively\.
+ [GetBuiltinIntent](API_GetBuiltinIntent.md), [GetBuiltinIntents](API_GetBuiltinIntents.md), and [GetBuiltinSlotTypes](API_GetBuiltinSlotTypes.md) to get an Amazon Lex built\-in intent, a list of Amazon Lex built\-in intents, or a list of built\-in slot types that you can use in your bot, respectively\.
+ [GetBotChannelAssociation](API_GetBotChannelAssociation.md) and [GetBotChannelAssociations](API_GetBotChannelAssociations.md) to get an association between your bot and a messaging platform or a list of the associations between your bot and messaging platforms, respectively\.
+ [DeleteBot](API_DeleteBot.md), [DeleteBotAlias](API_DeleteBotAlias.md), [DeleteBotChannelAssociation](API_DeleteBotChannelAssociation.md), [DeleteIntent](API_DeleteIntent.md), and [DeleteSlotType](API_DeleteSlotType.md) to remove unneeded resources in your account\.

You can use the model building API to create custom tools to manage your Amazon Lex resources\. For example, there is a limit of 100 versions each for bots, intents, and slot types\. You could use the model building API to build a tool that automatically deletes old versions when your bot nears the limit\.

To make sure that only one operation updates a resource at a time, Amazon Lex uses checksums\. When you use a `Put` API operation—[PutBot](API_PutBot.md), [PutBotAlias](API_PutBotAlias.md) [PutIntent](API_PutIntent.md), or [PutSlotType](API_PutSlotType.md)—to update a resource, you must pass the current checksum of the resource in the request\. If two tools try to update a resource at the same time, they both provide the same current checksum\. The first request to reach Amazon Lex matches the current checksum of the resource\. By the time that the second request arrives, the checksum is different\. The second tool receives a `PreconditionFailedException` exception and the update terminates\.

The `Get` operations—[GetBot](API_GetBot.md), [GetIntent](API_GetIntent.md), and [GetSlotType](API_GetSlotType.md)—are eventually consistent\. If you use a `Get` operation immediately after you create or modify a resource with one of the `Put` operations, the changes might not be returned\. After a `Get` operation returns the most recent update, it always returns that updated resource until the resource is modified again\. You can determine if an updated resource has been returned by looking at the checksum\.

## Runtime API Operations<a name="programming-model-runtime-api"></a>

 Client applications use the following runtime API operations to communicate with Amazon Lex: 
+ [PostContent](API_runtime_PostContent.md) – Takes speech or text input and returns intent information and a text or speech message to convey to the user\. Currently, Amazon Lex supports the following audio formats:

   

  Input audio formats – LPCM and Opus 

  Output audio formats – MPEG, OGG, and PCM

   

  The `PostContent` operation supports audio input at 8 kHz and 16 kHz\. Applications where the end user speaks with Amazon Lex over the telephone, such as an automated call center, can pass 8 kHz audio directly\. 

   
+ [PostText](API_runtime_PostText.md) – Takes text as input and returns intent information and a text message to convey to the user\.

Your client application uses the runtime API to call a specific Amazon Lex bot to process utterances — user text or voice input\. For example, suppose that a user says "I want pizza\." The client sends this user input to a bot using one of the Amazon Lex runtime API operations\. From the user input, Amazon Lex recognizes that the user request is for the `OrderPizza` intent defined in the bot\. Amazon Lex engages the user in a conversation to gather the required information, or slot data, such as pizza size, toppings, and number of pizzas\. After the user provides all of the necessary slot data, Amazon Lex either invokes the Lambda function code hook to fulfill the intent, or returns the intent data to the client, depending on how the intent is configured\.

Use the [PostContent](API_runtime_PostContent.md) operation when your bot uses speech input\. For example, an automated call center application can send speech to an Amazon Lex bot instead of an agent to address customer inquiries\. You can use the 8 kHz audio format to send audio directly from the telephone to Amazon Lex\.

The test window in the Amazon Lex console uses the [PostContent](API_runtime_PostContent.md) API to send text and speech requests to Amazon Lex\. You use this test window in the [Getting Started with Amazon Lex](getting-started.md) exercises\.

## Lambda Functions As Code Hooks<a name="prog-model-lambda"></a>

You can configure your Amazon Lex bot to invoke a Lambda function as a code hook\. The code hook can serve multiple purposes:
+ Customizes the user interaction—For example, when Joe asks for available pizza toppings, you can use prior knowledge of Joe's choices to display a subset of toppings\.
+ Validates the user's input—Suppose that Jen wants to pick up flowers after hours\. You can validate the time that Jen input and send an appropriate response\.
+ Fulfills the user's intent—After Joe provides all of the information for his pizza order, Amazon Lex can invoke a Lambda function to place the order with a local pizzeria\.

When you configure an intent, you specify Lambda functions as code hooks in the following places: 
+ Dialog code hook for initialization and validation—This Lambda function is invoked on each user input, assuming Amazon Lex understood the user intent\.
+ Fulfillment code hook—This Lambda function is invoked after the user provides all of the slot data required to fulfill the intent\.

You choose the intent and set the code hooks in the Amazon Lex console, as shown in the following screen shot:

![\[The Amazon Lex console showing Lambda function code hooks.\]](http://docs.aws.amazon.com/lex/latest/dg/images/how-works-10.png)

You can also set the code hooks using the `dialogCodeHook` and `fulfillmentActivity` fields in the [PutIntent](API_PutIntent.md) operation\.

One Lambda function can perform initialization, validation, and fulfillment\. The event data that the Lambda function receives has a field that identifies the caller as either a dialog or fulfillment code hook\. You can use this information to run the appropriate portion of your code\.

You can use a Lambda function to build a bot that can navigate complex dialogs\. You use the `dialogAction` field in the Lambda function response to direct Amazon Lex to take specific actions\. For example, you can use the `ElicitSlot` dialog action to tell Amazon Lex to ask the user for a slot value that isn't required\. If you have a clarification prompt defined, you can use the `ElicitIntent` dialog action to elicit a new intent when the user is finished with the previous one\.

For more information, see [Using Lambda Functions](using-lambda.md)\.