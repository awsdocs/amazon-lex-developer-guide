# MigrationSummary<a name="API_MigrationSummary"></a>

Provides information about migrating a bot from Amazon Lex V1 to Amazon Lex V2\.

## Contents<a name="API_MigrationSummary_Contents"></a>

 **migrationId**   <a name="lex-Type-MigrationSummary-migrationId"></a>
The unique identifier that Amazon Lex assigned to the migration\.  
Type: String  
Length Constraints: Fixed length of 10\.  
Pattern: `^[0-9a-zA-Z]+$`   
Required: No

 **migrationStatus**   <a name="lex-Type-MigrationSummary-migrationStatus"></a>
The status of the operation\. When the status is `COMPLETE` the bot is available in Amazon Lex V2\. There may be alerts and warnings that need to be resolved to complete the migration\.  
Type: String  
Valid Values:` IN_PROGRESS | COMPLETED | FAILED`   
Required: No

 **migrationStrategy**   <a name="lex-Type-MigrationSummary-migrationStrategy"></a>
The strategy used to conduct the migration\.  
Type: String  
Valid Values:` CREATE_NEW | UPDATE_EXISTING`   
Required: No

 **migrationTimestamp**   <a name="lex-Type-MigrationSummary-migrationTimestamp"></a>
The date and time that the migration started\.  
Type: Timestamp  
Required: No

 **v1BotLocale**   <a name="lex-Type-MigrationSummary-v1BotLocale"></a>
The locale of the Amazon Lex V1 bot that is the source of the migration\.  
Type: String  
Valid Values:` de-DE | en-AU | en-GB | en-IN | en-US | es-419 | es-ES | es-US | fr-FR | fr-CA | it-IT | ja-JP`   
Required: No

 **v1BotName**   <a name="lex-Type-MigrationSummary-v1BotName"></a>
The name of the Amazon Lex V1 bot that is the source of the migration\.  
Type: String  
Length Constraints: Minimum length of 2\. Maximum length of 50\.  
Pattern: `^([A-Za-z]_?)+$`   
Required: No

 **v1BotVersion**   <a name="lex-Type-MigrationSummary-v1BotVersion"></a>
The version of the Amazon Lex V1 bot that is the source of the migration\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 64\.  
Pattern: `\$LATEST|[0-9]+`   
Required: No

 **v2BotId**   <a name="lex-Type-MigrationSummary-v2BotId"></a>
The unique identifier of the Amazon Lex V2 that is the destination of the migration\.  
Type: String  
Length Constraints: Fixed length of 10\.  
Pattern: `^[0-9a-zA-Z]+$`   
Required: No

 **v2BotRole**   <a name="lex-Type-MigrationSummary-v2BotRole"></a>
The IAM role that Amazon Lex uses to run the Amazon Lex V2 bot\.  
Type: String  
Length Constraints: Minimum length of 20\. Maximum length of 2048\.  
Pattern: `^arn:[\w\-]+:iam::[\d]{12}:role/.+$`   
Required: No

## See Also<a name="API_MigrationSummary_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/lex-models-2017-04-19/MigrationSummary) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/lex-models-2017-04-19/MigrationSummary) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/lex-models-2017-04-19/MigrationSummary) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/lex-models-2017-04-19/MigrationSummary) 