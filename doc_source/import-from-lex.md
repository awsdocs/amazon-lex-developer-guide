# Importing in Amazon Lex Format<a name="import-from-lex"></a>

After you have exported a resource to a JSON file in the Amazon Lex format, you can import the JSON file containing the resource into one or more AWS accounts\. For example, you can export a bot, and then import it into another AWS Region\. Or you can send the bot to a colleague so that she can import it into her account\. 

When you import a bot, intent, or slot type, you must decide whether you want to overwrite the `$LATEST` version of a resource, such as an intent or a slot type, during import, or if you want the import to fail if you want to preserve the resource that is in your account\. For example, if you are uploading an edited version of a resource to your account, you would choose to overwrite the `$LATEST` version\. If you are uploading a resource sent to you by a colleague, you can choose to have the import fail if there are are resource conflicts so that your own resources aren't replaced\.

When importing a resource, the permissions assigned to the user making the import request apply\. The user must have permissions for all of the resources in the account that the import affects\. The user must also have permission for the [GetBot](API_GetBot.md), [PutBot](API_PutBot.md), [GetIntent](API_GetIntent.md) [PutIntent](API_PutIntent.md), [GetSlotType](API_GetSlotType.md), [PutSlotType](API_PutSlotType.md) operations\. For more information about permissions, see [How Amazon Lex Works with IAM](security_iam_service-with-iam.md)\.

The import reports errors that occur during processing\. Some errors are reported before the import begins, others are reported during the import process\. For example, if the account that is importing an intent doesn't have permission to call a Lambda function that the intent uses, the import fails before changes are made to the slot types or intents\. If an import fails during the import process, the `$LATEST` version of any intent or slot type imported before the process failed is modified\. You can't roll back changes made to the `$LATEST` version\.

When you import a resource, all dependent resources are imported to the `$LATEST` version of the resource and then given a numbered version\. For example, if a bot uses an intent, the intent is given a numbered version\. If an intent uses a custom slot type, the slot type is given a numbered version\.

A resource is imported only once\. For example, if the bot contains an `OrderPizza` intent and an `OrderDrink` intent that both rely on the custom slot type `Size`, the `Size` slot type is imported once and used for both intents\.

**Note**  
If you exported your bot with the `enableModelImprovements` parameter set to `false`, you must open the \.zip file containing the bot definition and change the `enableModelImprovements` parameter to `true` in the following Regions:  
Asia Pacific \(Singapore\) \(ap\-southeast\-1\)
Asia Pacific \(Tokyo\) \(ap\-northeast\-1\)
EU \(Frankfurt\) \(eu\-central\-1\)
EU \(London\) \(eu\-west\-2\)

The process for importing a bot, an intent, or a custom slot type is the same\. In the following procedures, substitute intent or slot type, as appropriate\. 

## Importing a Bot<a name="import-console"></a>

**To import a bot**

1. Sign in to the AWS Management Console, and open the Amazon Lex console at [https://console\.aws\.amazon\.com/lex/](https://console.aws.amazon.com/lex/)\. 

1. Choose **Bots**, then choose the bot to import\. To import a new bot, skip this step\.

1. For **Actions**, choose **Import**\.

1. For **Import Bot**, choose the \.zip archive that contains the JSON file that contains the bot to import\. If you want to see merge conflicts before merging, choose **Notify me of merge conflicts**\. If you turn off conflict checking, the `$LATEST` version of all of the resources used by the bot are overwritten\.

1. Choose **Import**\. If you have chosen to be notified of merge conflicts and there are conflicts, a dialog appears that lists them\. To overwrite the `$LATEST` version of all conflicting resources, choose **Overwrite and continue**\. To stop the import, choose **Cancel**\.

You can now test the bot in your account\. 