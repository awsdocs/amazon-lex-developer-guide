# Exporting in Amazon Lex Format<a name="export-to-lex"></a>

Export your Amazon Lex bots, intents, and slot types to a format that you can import to an AWS account\. You can export the following resources:
+ A bot, including all of the intents and custom slot types used by the bot
+ An intent, including all of the custom slot types used by the intent
+ A custom slot type, including all of values for the slot type

You can export only a numbered version of a resource\. You can't export a resource's `$LATEST` version\.

Exporting is an asynchronous process\. When the export is complete, you get an Amazon S3 presigned URL\. The URL provides the location of a \.zip archive that contains the exported resource in JSON format\. 

You use either the console or the [GetExport](API_GetExport.md) operation to export bots, intents, and custom slot types\. 

The process for exporting, a bot, an intent, or a slot type is the same\. In the following procedures, substitute intent or slot type for bot\. 

## Exporting a Bot<a name="export-console"></a>

**To export a bot**

1. Sign in to the AWS Management Console, and open the Amazon Lex console at [https://console\.aws\.amazon\.com/lex/](https://console.aws.amazon.com/lex/)\. 

1. Choose **Bots**, then choose the bot to export\.

1. On the **Actions** menu, choose **Export**\.

1. In the **Export Bot** dialog, choose the version of the bot to export\. For **Platform**, choose **Amazon Lex**\.

1. Choose **Export**\.

1. Download and save the \.zip archive\.

Amazon Lex exports the bot to a JSON file that is contained in the \.zip archive\. To update the bot, modify the JSON text, then import it back into Amazon Lex\.

**Next step**  
[Importing in Amazon Lex Format](import-from-lex.md)