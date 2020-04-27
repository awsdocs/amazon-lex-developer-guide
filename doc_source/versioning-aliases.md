# Versioning and Aliases<a name="versioning-aliases"></a>

Amazon Lex supports publishing versions of bots, intents, and slot types so that you can control the implementation that your client applications use\. A *version* is a numbered snapshot of your work that you can publish for use in different parts of your workflow, such as development, beta deployment, and production\.

Amazon Lex bots also support aliases\. An *alias* is a pointer to a specific version of a bot\. With an alias, you can easily update the version that your client applications are using\. For example, you can point an alias to version 1 of your bot\. When you are ready to update the bot, you publish version 2 and change the alias to point to the new version\. Because your applications use the alias instead of a specific version, all of your clients get the new functionality without needing to be updated\.

**Topics**
+ [Versioning](#versioning-intro)
+ [Aliases](#aliases-intro)

## Versioning<a name="versioning-intro"></a>

When you version an Amazon Lex resource you create a snapshot of the resource so that you can use the resource as it existed when the version was made\. Once you've created a version it will stay the same while you continue to work on your application\.

### The $LATEST Version<a name="versioning-intro-create-function"></a>

When you create an Amazon Lex bot, intent, or slot type there is only one version, the `$LATEST` version\. 

![\[The $LATEST version of a bot.\]](http://docs.aws.amazon.com/lex/latest/dg/images/lex-only-bot.png)

`$LATEST` is the working copy of your resource\. You can update only the `$LATEST` version and until you publish your first version, `$LATEST` is the only version of the resource that you have\. 

Only the `$LATEST` version of a resource can use the `$LATEST` version of another resource\. For example, the `$LATEST` version of a bot can use the `$LATEST` version of an intent, and the `$LATEST` version of an intent can use the `$LATEST` version of a slot type\.

The `$LATEST` version of your bot should only be used for manual testing\. Amazon Lex limits the number of runtime requests that you can make to the `$LATEST` version of the bot\.

### Publishing an Amazon Lex Resource Version<a name="versioning-intro-publish-version"></a>

When you publish a resource, Amazon Lex makes a copy of the `$LATEST` version and saves it as a numbered version\. The published version can't be changed\. 

![\[Publishing a new version of the bot.\]](http://docs.aws.amazon.com/lex/latest/dg/images/bot2.png) 

You create and publish versions using the Amazon Lex console or the [CreateBotVersion](API_CreateBotVersion.md) operation\. For an example, see [Exercise 3: Publish a Version and Create an Alias](gettingstarted-ex3.md)\. 

When you modify the `$LATEST` version of a resource, you can publish the new version to make the changes available to your client applications\. Every time you publish a version, Amazon Lex copies the `$LATEST` version to create the new version and increments the version number by 1\. Version numbers are never reused\. For example, if you remove a resource numbered version 10 and then recreate it, the next version number Amazon Lex assigns is version 11\.

Before you can publish a bot, you must point it to a numbered version of any intent that it uses\. If you try to publish a new version of a bot that uses the $LATEST version of an intent, Amazon Lex returns an HTTP 400 Bad Request exception\. Before you can publish a numbered version of the intent, you must point the intent to a numbered version of any slot type that it uses\. Otherwise you will get an HTTP 400 Bad Request exception\.

![\[Publishing a new version of $LATEST.\]](http://docs.aws.amazon.com/lex/latest/dg/images/lex-publish-identical-bot.png) 

**Note**  
Amazon Lex publishes a new version only if the last published version is different from the `$LATEST` version\. If you try to publish the `$LATEST` version without modifying it, Amazon Lex doesn't create or publish a new version\. 

### Updating an Amazon Lex Resource<a name="versioning-intro-updating-function-code"></a>

You can update only the `$LATEST` version of an Amazon Lex bot, intent, or slot type\. Published versions can't be changed\. You can publish a new version any time after you update a resource in the console or with the [CreateBotVersion](API_CreateBotVersion.md), the [CreateIntentVersion](API_CreateIntentVersion.md) or the [CreateSlotTypeVersion](API_CreateSlotTypeVersion.md) operations\.

### Deleting an Amazon Lex Resource or Version<a name="versioning-intro-deleting-function-versions"></a>

Amazon Lex supports deleting a resource or version using the console or one of the API operations:
+ [DeleteBot](API_DeleteBot.md)
+ [DeleteBotVersion](API_DeleteBotVersion.md)
+ [DeleteBotAlias](API_DeleteBotAlias.md)
+ [DeleteBotChannelAssociation](API_DeleteBotChannelAssociation.md)
+ [DeleteIntent](API_DeleteIntent.md)
+ [DeleteIntentVersion](API_DeleteIntentVersion.md)
+ [DeleteSlotType](API_DeleteSlotType.md)
+ [DeleteSlotTypeVersion](API_DeleteSlotTypeVersion.md)

## Aliases<a name="aliases-intro"></a>

An alias is a pointer to a specific version of an Amazon Lex bot\. Use an alias to allow client applications to use a specific version of the bot without requiring the application to track which version that is\.

The following example shows two versions of an Amazon Lex bot, version version 1 and version 2\. Each of these bot versions has an associated alias, BETA and PROD, respectively\. Client applications use the PROD alias to access the bot\.

![\[Point a client application to a version by using an alias.\]](http://docs.aws.amazon.com/lex/latest/dg/images/lex-publish-alias-bot.png) 

When you create a second version of the bot, you can update the alias to point to the new version of the bot using the console or the [PutBot](API_PutBot.md) operation\. When you change the alias, all of your client applications use the new version\. If there is a problem with the new version, you can roll back to the previous version by simply changing the alias to point to that version\.

![\[Updating an alias changes the version used by client applications.\]](http://docs.aws.amazon.com/lex/latest/dg/images/lex-publish-alias-bot-v2.png) 

**Note**  
Although you can test the `$LATEST` version of a bot in the console, we recommend that when you integrate a bot with your client application, you first publish a version and create an alias that points to that version\. Use the alias in your client application for the reasons explained in this section\. When you update an alias, Amazon Lex will wait until the session timeout of all current sessions expires before it starts using the new version\. For more information about the session timeout, see [Setting the Session Timeout](context-mgmt.md#context-mgmt-session-timeout)