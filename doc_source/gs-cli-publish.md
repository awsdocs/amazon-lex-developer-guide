# Exercise 4: Publish a Version \(AWS CLI\)<a name="gs-cli-publish"></a>

Now, create a version of the bot that you created in Exercise 1\. A *version* is a snapshot of the bot\. After you create a version, you can’t change it\. The only version of a bot that you can update is the `$LATEST` version\. For more information about versions, see [Versioning and Aliases](versioning-aliases.md)\. 

Before you can publish a version of a bot, you must publish the intents that is uses\. Likewise, you must publish the slot types that those intents refer to\. In general, to publish a version of a bot, you do the following:

1. Publish a version of a slot type with the [CreateSlotTypeVersion](API_CreateSlotTypeVersion.md) operation\.

1. Publish a version of an intent with the [CreateIntentVersion](API_CreateIntentVersion.md) operation\.

1. Publish a version of a bot with the [CreateBotVersion](API_CreateBotVersion.md) operation \.

To run the commands in this exercise, you need to know the region where the commands will be run\. For a list of regions, see [ Model Building Quotas ](gl-limits.md#gl-limits-model-building)\.

**Topics**
+ [Step 1: Publish the Slot Type \(AWS CLI\)](gs-cli-publish-slot-type.md)
+ [Step 2: Publish the Intent \(AWS CLI\)](gs-cli-publish-intent.md)
+ [Step 3: Publish the Bot \(AWS CLI\)](gs-cli-publish-bot.md)