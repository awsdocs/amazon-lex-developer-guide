# Exercise 1: Create an Amazon Lex Bot \(AWS CLI\)<a name="gs-cli-create"></a>

In general, when you create bots, you:

1. Create slot types to define the information that your bot will be working with\.

1. Create intents that define the user actions that your bot supports\. Use the custom slot types that you created earlier to define the slots, or parameters, that your intent requires\.

1. Create a bot that uses the intents that you defined\. 

In this exercise you create and test a new Amazon Lex bot using the CLI\. Use the JSON structures that we provide to create the bot\. To run the commands in this exercise, you need to know the region where the commands will be run\. For a list of regions, see [ Model Building Quotas ](gl-limits.md#gl-limits-model-building)\.

**Topics**
+ [Step 1: Create a Service\-Linked Role \(AWS CLI\)](gs-create-role.md)
+ [Step 2: Create a Custom Slot Type \(AWS CLI\)](gs-create-flower-types.md)
+ [Step 3: Create an Intent \(AWS CLI\)](gs-cli-create-order-flowers.md)
+ [Step 4: Create a Bot \(AWS CLI\)](gs-cli-create-order-flowers-bot.md)
+ [Step 5: Test a Bot \(AWS CLI\)](gs-create-test.md)