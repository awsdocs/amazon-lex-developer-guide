# Importing and Exporting Amazon Lex Bots, Intents, and Slot Types<a name="import-export"></a>

You can import or export a bot, intent, or slot type\. For example, if you want to share a bot with a colleague in a different AWS account, you can export it, then send it to her\. If you want to add multiple utterances to a bot, you can export it, add the utterances, then import it back into your account\. 

You can *export* bots, intents, and slot types in either Amazon Lex \(to share or modify them\) or an Alexa skill format\. You can *import* only in Amazon Lex format\. 

When you export a resource, you have to export it in a format that is compatible with the service that you are exporting to, Amazon Lex or the Alexa Skills Kit\. If you export a bot in Amazon Lex format, you can reimport it into your account, or an Amazon Lex user in another account can import it into his account\. You can also export a bot in a format compatible with an Alexa skill\. Then you can import the bot using the Alexa Skills Kit to make your bot available with Alexa\. For more information, see [Exporting to an Alexa Skill](export-to-alexa.md)\.

When you export a bot, intent or slot type, its resources are written to a JSON file\. To export a bot, intent, or slot type, you can use either the Amazon Lex console or the [GetExport](API_GetExport.md) operation\. Import a bot, intent or slot type using the [StartImport](API_StartImport.md)\. 

**Topics**
+ [Exporting and Importing in Amazon Lex Format](import-export-lex.md)
+ [Exporting to an Alexa Skill](export-to-alexa.md)