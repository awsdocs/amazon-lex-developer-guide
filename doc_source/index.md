# Amazon Lex Developer Guide

-----
*****Copyright &copy; 2018 Amazon Web Services, Inc. and/or its affiliates. All rights reserved.*****

-----
Amazon's trademarks and trade dress may not be used in 
     connection with any product or service that is not Amazon's, 
     in any manner that is likely to cause confusion among customers, 
     or in any manner that disparages or discredits Amazon. All other 
     trademarks not owned by Amazon are the property of their respective
     owners, who may or may not be affiliated with, connected to, or 
     sponsored by Amazon.

-----
## Contents
+ [What Is Amazon Lex?](what-is.md)
+ [Amazon Lex: How It Works](how-it-works.md)
   + [Programming Model](programming-model.md)
   + [Service Permissions](howitworks-service-permissions.md)
   + [Managing Messages](howitworks-manage-prompts.md)
   + [Managing Conversation Context](context-mgmt.md)
   + [Bot Deployment Options](chatbot-service.md)
   + [Built-in Intents and Slot Types](howitworks-builtins.md)
      + [Built-in Intents](howitworks-builtins-intents.md)
      + [Built-in Slot Types](howitworks-builtins-slots.md)
         + [Alexa Skills Kit Slot Types](built-in-alexa.md)
         + [AMAZON.EmailAddress](built-in-slot-email.md)
         + [AMAZON.NUMBER](built-in-slot-number.md)
         + [AMAZON.Percentage](built-in-slot-percent.md)
         + [AMAZON.PhoneNumber](built-in-slot-phone.md)
         + [AMAZON.SpeedUnit](built-in-slot-speed.md)
         + [AMAZON.TIME](built-in-slot-time.md)
         + [AMAZON.WeightUnit](built-in-slot-weight.md)
   + [Custom Slot Types](howitworks-custom-slots.md)
+ [Getting Started with Amazon Lex](getting-started.md)
   + [Step 1: Set Up an AWS Account and Create an Administrator User](gs-account.md)
   + [Step 2: Set Up the AWS Command Line Interface](gs-set-up-cli.md)
   + [Step 3: Getting Started (Console)](gs-console.md)
      + [Exercise 1: Create an Amazon Lex Bot Using a Blueprint (Console)](gs-bp.md)
         + [Step 1: Create an Amazon Lex Bot (Console)](gs-bp-create-bot.md)
         + [Step 2 (Optional): Review the Details of Information Flow (Console)](gs-bp-details-two-runtime-apis.md)
            + [Step 2a (Optional): Review the Details of the Spoken Information Flow (Console)](gs-bp-details-postcontent-flow.md)
            + [Step 2b (Optional): Review the Details of the Typed Information Flow (Console)](gs-bp-details-part1.md)
         + [Step 3: Create a Lambda Function (Console)](gs-bp-create-lambda-function.md)
         + [Step 4: Add the Lambda Function as Code Hook (Console)](gs-bp-create-integrate.md)
         + [Step 5 (Optional): Review the Details of the Information Flow (Console)](gs-bp-details-after-lambda.md)
         + [Step 6: Update the Intent Configuration to Add an Utterance (Console)](gs-bp-utterance.md)
         + [Step 7 (Optional): Clean Up (Console)](gs-bp-cleaning-up.md)
      + [Exercise 2: Create a Custom Amazon Lex Bot](getting-started-ex2.md)
         + [Step 1: Create a Lambda Function](gs2-prepare.md)
         + [Step 2: Create a Bot](gs2-create-bot.md)
            + [Create the Bot](gs2-create-bot-create.md)
            + [Create an Intent](gs2-create-bot-intent.md)
            + [Create Slot Types](gs2-create-bot-slot-types.md)
            + [Configure the Intent](gs2-create-bot-configure-intent.md)
            + [Configure the Bot](gs2-create-bot-configure-bot.md)
         + [Step 3: Build and Test the Bot](gs2-build-and-test.md)
         + [Step 4 (Optional): Clean up](gs2-clean-up.md)
      + [Exercise 3: Publish a Version and Create an Alias](gettingstarted-ex3.md)
   + [Step 4: Getting Started (AWS CLI)](gs-cli.md)
      + [Exercise 1: Create an Amazon Lex Bot (AWS CLI)](gs-cli-create.md)
         + [Step 1: Create a Service-Linked Role (AWS CLI)](gs-create-role.md)
         + [Step 2: Create a Custom Slot Type (AWS CLI)](gs-create-flower-types.md)
            + [FlowerTypes.json](gs-cli-create-flower-types-json.md)
         + [Step 3: Create an Intent (AWS CLI)](gs-cli-create-order-flowers.md)
            + [OrderFlowers.json](gs-cli-create-order-flowers-json.md)
         + [Step 4: Create a Bot (AWS CLI)](gs-cli-create-order-flowers-bot.md)
            + [OrderFlowersBot.json](gs-cli-create-order-flowers-bot-json.md)
         + [Step 5: Test a Bot (AWS CLI)](gs-create-test.md)
            + [Test the Bot Using Text Input (AWS CLI)](gs-create-test-text.md)
            + [Test the Bot Using Speech Input (AWS CLI)](gs-create-test-speech.md)
      + [Exercise 2: Add a New Utterance (AWS CLI)](gs-cli-update-utterance.md)
      + [Exercise 3: Add a Lambda Function (AWS CLI)](gs-cli-update-lambda.md)
      + [Exercise 4: Publish a Version (AWS CLI)](gs-cli-publish.md)
         + [Step 1: Publish the Slot Type (AWS CLI)](gs-cli-publish-slot-type.md)
         + [Step 2: Publish the Intent (AWS CLI)](gs-cli-publish-intent.md)
         + [Step 3: Publish the Bot (AWS CLI)](gs-cli-publish-bot.md)
      + [Exercise 5: Create an Alias (AWS CLI)](gs-cli-create-alias.md)
      + [Exercise 6: Clean Up (AWS CLI)](gs-cli-clean-up.md)
+ [Versioning and Aliases](versioning-aliases.md)
+ [Using Lambda Functions](using-lambda.md)
   + [Lambda Function Input Event and Response Format](lambda-input-response-format.md)
   + [Amazon Lex and AWS Lambda Blueprints](lex-lambda-blueprints.md)
+ [Deploying Amazon Lex Bots](examples.md)
   + [Deploying an Amazon Lex Bot on a Messaging Platform](example1.md)
      + [Integrating an Amazon Lex Bot with Facebook Messenger](fb-bot-association.md)
      + [Integrating an Amazon Lex Bot with Kik](kik-bot-association.md)
         + [Step 1: Create an Amazon Lex Bot](kik-bot-assoc-create-bot.md)
         + [Step 2: Create a Kik Bot](kik-bot-assoc-create-kik-bot.md)
         + [Step 3: Integrate the Kik Bot with the Amazon Lex Bot](kik-bot-assoc-create-assoc.md)
         + [Step 4: Test the Integration](kik-bot-assoc-test.md)
      + [Integrating an Amazon Lex Bot with Slack](slack-bot-association.md)
         + [Step 1: Create an Amazon Lex Bot](slack-bot-assoc-create-bot.md)
         + [Step 2: Sign Up for Slack and Create a Slack Team](slack-bot-assoc-create-team.md)
         + [Step 3: Create a Slack Application](slack-bot-assoc-create-app.md)
         + [Step 4: Integrate the Slack Application with the Amazon Lex Bot](slack-bot-assoc-create-assoc.md)
         + [Step 5: Complete Slack Integration](slack-bot-back-in-slack-console.md)
         + [Step 6: Test the Integration](slack-bot-test.md)
      + [Integrating an Amazon Lex Bot with Twilio Programmable SMS](twilio-bot-association.md)
   + [Deploying an Amazon Lex Bot in Mobile Applications](example2.md)
+ [Importing and Exporting Amazon Lex Bots, Intents, and Slot Types](import-export.md)
   + [Exporting and Importing in Amazon Lex Format](import-export-lex.md)
      + [Exporting in Amazon Lex Format](export-to-lex.md)
      + [Importing in Amazon Lex Format](import-from-lex.md)
      + [JSON Format for Importing and Exporting](import-export-format.md)
   + [Exporting to an Alexa Skill](export-to-alexa.md)
+ [Additional Examples: Creating Amazon Lex Bots](additional-exercises.md)
   + [Example Bot: ScheduleAppointment](ex1-sch-appt.md)
      + [Step 1: Create an Amazon Lex Bot](ex1-sch-appt-create-bot.md)
      + [Step 2: Create a Lambda Function](ex1-sch-appt-create-lambda-function.md)
      + [Step 3: Update the Intent: Configure a Code Hook](ex1-sch-appt-create-integrate.md)
      + [Step 4: Deploy the Bot on the Facebook Messenger Platform](ex-sch-appt-fb-integration.md)
      + [Details of Information Flow](ex1-sch-appt-info-flow-details.md)
   + [Example Bot: BookTrip](ex-book-trip.md)
      + [Step 1: Review the Blueprints Used in this Exercise](ex-book-trip-blueprints.md)
      + [Step 2: Create an Amazon Lex Bot](ex-book-trip-create-bot.md)
      + [Step 3: Create a Lambda function](ex-book-trip-create-lambda-function.md)
      + [Step 4: Add the Lambda Function as a Code Hook](ex-book-trip-create-integrate.md)
      + [Details of the Information Flow](book-trip-detail-flow.md)
   + [Example: Using a Response Card](ex-resp-card.md)
   + [Example: Updating Utterances](ex-utterances.md)
   + [Example: Integrating with a Web site](ex-web.md)
+ [Monitoring Amazon Lex](monitoring-aws-lex.md)
   + [Monitoring Amazon Lex with Amazon CloudWatch](monitoring-aws-lex-cloudwatch.md)
      + [CloudWatch Metrics for Amazon Lex](aws-lex-cloudwatch-dimensions.md)
   + [Monitoring Amazon Lex API Calls with AWS CloudTrail Logs](monitoring-aws-lex-cloudtrail.md)
+ [Guidelines and Limits in Amazon Lex](guidelines-and-limits.md)
   + [General Guidelines](gl-guidelines.md)
   + [Limits](gl-limits.md)
+ [Authentication and Access Control for Amazon Lex](auth-and-access-control.md)
   + [Overview of Managing Access Permissions to Your Amazon Lex Resources](access-control-overview.md)
   + [Using Identity-Based Policies (IAM Policies) for Amazon Lex](access-control-managing-permissions.md)
   + [Amazon Lex API Permissions: Actions, Resources, and Conditions Reference](lex-api-permissions-ref.md)
+ [API Reference](API_Reference.md)
   + [Actions](API_Operations.md)
      + [Amazon Lex Model Building Service](API_Operations_Amazon_Lex_Model_Building_Service.md)
         + [CreateBotVersion](API_CreateBotVersion.md)
         + [CreateIntentVersion](API_CreateIntentVersion.md)
         + [CreateSlotTypeVersion](API_CreateSlotTypeVersion.md)
         + [DeleteBot](API_DeleteBot.md)
         + [DeleteBotAlias](API_DeleteBotAlias.md)
         + [DeleteBotChannelAssociation](API_DeleteBotChannelAssociation.md)
         + [DeleteBotVersion](API_DeleteBotVersion.md)
         + [DeleteIntent](API_DeleteIntent.md)
         + [DeleteIntentVersion](API_DeleteIntentVersion.md)
         + [DeleteSlotType](API_DeleteSlotType.md)
         + [DeleteSlotTypeVersion](API_DeleteSlotTypeVersion.md)
         + [DeleteUtterances](API_DeleteUtterances.md)
         + [GetBot](API_GetBot.md)
         + [GetBotAlias](API_GetBotAlias.md)
         + [GetBotAliases](API_GetBotAliases.md)
         + [GetBotChannelAssociation](API_GetBotChannelAssociation.md)
         + [GetBotChannelAssociations](API_GetBotChannelAssociations.md)
         + [GetBots](API_GetBots.md)
         + [GetBotVersions](API_GetBotVersions.md)
         + [GetBuiltinIntent](API_GetBuiltinIntent.md)
         + [GetBuiltinIntents](API_GetBuiltinIntents.md)
         + [GetBuiltinSlotTypes](API_GetBuiltinSlotTypes.md)
         + [GetExport](API_GetExport.md)
         + [GetImport](API_GetImport.md)
         + [GetIntent](API_GetIntent.md)
         + [GetIntents](API_GetIntents.md)
         + [GetIntentVersions](API_GetIntentVersions.md)
         + [GetSlotType](API_GetSlotType.md)
         + [GetSlotTypes](API_GetSlotTypes.md)
         + [GetSlotTypeVersions](API_GetSlotTypeVersions.md)
         + [GetUtterancesView](API_GetUtterancesView.md)
         + [PutBot](API_PutBot.md)
         + [PutBotAlias](API_PutBotAlias.md)
         + [PutIntent](API_PutIntent.md)
         + [PutSlotType](API_PutSlotType.md)
         + [StartImport](API_StartImport.md)
      + [Amazon Lex Runtime Service](API_Operations_Amazon_Lex_Runtime_Service.md)
         + [PostContent](API_runtime_PostContent.md)
         + [PostText](API_runtime_PostText.md)
   + [Data Types](API_Types.md)
      + [Amazon Lex Model Building Service](API_Types_Amazon_Lex_Model_Building_Service.md)
         + [BotAliasMetadata](API_BotAliasMetadata.md)
         + [BotChannelAssociation](API_BotChannelAssociation.md)
         + [BotMetadata](API_BotMetadata.md)
         + [BuiltinIntentMetadata](API_BuiltinIntentMetadata.md)
         + [BuiltinIntentSlot](API_BuiltinIntentSlot.md)
         + [BuiltinSlotTypeMetadata](API_BuiltinSlotTypeMetadata.md)
         + [CodeHook](API_CodeHook.md)
         + [EnumerationValue](API_EnumerationValue.md)
         + [FollowUpPrompt](API_FollowUpPrompt.md)
         + [FulfillmentActivity](API_FulfillmentActivity.md)
         + [Intent](API_Intent.md)
         + [IntentMetadata](API_IntentMetadata.md)
         + [Message](API_Message.md)
         + [Prompt](API_Prompt.md)
         + [ResourceReference](API_ResourceReference.md)
         + [Slot](API_Slot.md)
         + [SlotTypeMetadata](API_SlotTypeMetadata.md)
         + [Statement](API_Statement.md)
         + [UtteranceData](API_UtteranceData.md)
         + [UtteranceList](API_UtteranceList.md)
      + [Amazon Lex Runtime Service](API_Types_Amazon_Lex_Runtime_Service.md)
         + [Button](API_runtime_Button.md)
         + [GenericAttachment](API_runtime_GenericAttachment.md)
         + [ResponseCard](API_runtime_ResponseCard.md)
+ [Document History for Amazon Lex](doc-history.md)
+ [AWS Glossary](glossary.md)