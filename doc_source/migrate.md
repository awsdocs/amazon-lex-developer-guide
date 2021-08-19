# Migrating a bot<a name="migrate"></a>

The Amazon Lex V2 API uses an updated information architecture that enables simplified resource versioning and support for multiple languages in a bot\. For more information, see the [Migration guide](https://docs.aws.amazon.com/lexv2/latest/dg/migration.html) in the *Amazon Lex V2 Developer Guide*\. 

To use these new features, you need to migrate your bot\. When you migrate a bot, Amazon Lex provides the following:
+ Migration copies your custom intents and slot types to the Amazon Lex V2 bot\. 
+ You can add multiple languages to the same Amazon Lex V2 bot\. In Amazon Lex V1 you create a separate bot for each language\. You can migrate multiple Amazon Lex V1 bots, each using a different language, to one Amazon Lex V2 bot\.
+ Amazon Lex maps Amazon Lex V1 built\-in slot types and intents to Amazon Lex V2 built\-in slot types and intents\. If a built\-in can't be migrated, Amazon Lex returns a message that tells you what to do next\.

The migration process doesn't migrate the following:
+ Aliases
+ Amazon Kendra indexes
+ AWS Lambda functions
+ Conversation log settings
+ Messaging channels such as Slack
+ Tags

To migrate a bot, your user or role must have IAM permission for both Amazon Lex and Amazon Lex V2 API operations\. For the required permissions, see [Example: Allow a user to migrate a bot to Amazon Lex V2 APIs](security_iam_id-based-policy-examples.md#security_iam_id-based-policy-examples-migrate)\.

## Migrating a bot \(Console\)<a name="migrating-a-bot"></a>

Use the Amazon Lex V1 console to migrate the structure of a bot to an Amazon Lex V2 bot\.

**To use the console to migrate a bot to the Amazon Lex V2 API**

1. Sign in to the AWS Management Console and open the Amazon Lex console at [https://console\.aws\.amazon\.com/lex/](https://console.aws.amazon.com/lex/)\.

1. From the left menu, choose **Migration tool**\.

1. From the list of bots, choose the bot that you want to migrate and then choose **Migrate**\.

1. Choose the version of the bot that you want to migrate, then enter the name of the bot to migrate to\. If you enter the name of an existing Amazon Lex V2 bot, the Amazon Lex V1 bot is migrated to the language shown in the details and overwrites the Draft version of the language\.

1. Choose **Next**\.

1. Choose the IAM role that Amazon Lex uses to run the Amazon Lex V2 API version of the bot\. You can choose to create a new role with the minimum permissions required to run the bot, or you can choose an existing IAM role\.

1. Choose **Next**\.

1. Review the settings for migration\. If they look OK, choose **Start migration**\.

After you start the migration process, you are returned to the migration tool start page\. You can monitor the progress of the migration in the **History** table\. When the **Migration status** column says **Complete** the migration is finished\. 

Amazon Lex uses the `StartImport` operation in the Amazon Lex V2 API to import the migrated bot\. You'll see an entry in the Amazon Lex V2 console import history table for each migration\.

During the migration, Amazon Lex may find resources in the bot that can't be migrated\. You get an error or warning message for each resource that can't be migrated\. Each message includes a link to documentation that explains how to resolve the issue\. 