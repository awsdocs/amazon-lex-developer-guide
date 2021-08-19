# StartMigration<a name="API_StartMigration"></a>

Starts migrating a bot from Amazon Lex V1 to Amazon Lex V2\. Migrate your bot when you want to take advantage of the new features of Amazon Lex V2\.

For more information, see [Migrating a bot](https://docs.aws.amazon.com/lex/latest/dg/migrate.html) in the *Amazon Lex developer guide*\.

## Request Syntax<a name="API_StartMigration_RequestSyntax"></a>

```
POST /migrations HTTP/1.1
Content-type: application/json

{
   "migrationStrategy": "string",
   "v1BotName": "string",
   "v1BotVersion": "string",
   "v2BotName": "string",
   "v2BotRole": "string"
}
```

## URI Request Parameters<a name="API_StartMigration_RequestParameters"></a>

The request does not use any URI parameters\.

## Request Body<a name="API_StartMigration_RequestBody"></a>

The request accepts the following data in JSON format\.

 ** [migrationStrategy](#API_StartMigration_RequestSyntax) **   <a name="lex-StartMigration-request-migrationStrategy"></a>
The strategy used to conduct the migration\.  
+  `CREATE_NEW` \- Creates a new Amazon Lex V2 bot and migrates the Amazon Lex V1 bot to the new bot\.
+  `UPDATE_EXISTING` \- Overwrites the existing Amazon Lex V2 bot metadata and the locale being migrated\. It doesn't change any other locales in the Amazon Lex V2 bot\. If the locale doesn't exist, a new locale is created in the Amazon Lex V2 bot\.
Type: String  
Valid Values:` CREATE_NEW | UPDATE_EXISTING`   
Required: Yes

 ** [v1BotName](#API_StartMigration_RequestSyntax) **   <a name="lex-StartMigration-request-v1BotName"></a>
The name of the Amazon Lex V1 bot that you are migrating to Amazon Lex V2\.  
Type: String  
Length Constraints: Minimum length of 2\. Maximum length of 50\.  
Pattern: `^([A-Za-z]_?)+$`   
Required: Yes

 ** [v1BotVersion](#API_StartMigration_RequestSyntax) **   <a name="lex-StartMigration-request-v1BotVersion"></a>
The version of the bot to migrate to Amazon Lex V2\. You can migrate the `$LATEST` version as well as any numbered version\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 64\.  
Pattern: `\$LATEST|[0-9]+`   
Required: Yes

 ** [v2BotName](#API_StartMigration_RequestSyntax) **   <a name="lex-StartMigration-request-v2BotName"></a>
The name of the Amazon Lex V2 bot that you are migrating the Amazon Lex V1 bot to\.   
+ If the Amazon Lex V2 bot doesn't exist, you must use the `CREATE_NEW` migration strategy\.
+ If the Amazon Lex V2 bot exists, you must use the `UPDATE_EXISTING` migration strategy to change the contents of the Amazon Lex V2 bot\.
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `^([0-9a-zA-Z][_-]?)+$`   
Required: Yes

 ** [v2BotRole](#API_StartMigration_RequestSyntax) **   <a name="lex-StartMigration-request-v2BotRole"></a>
The IAM role that Amazon Lex uses to run the Amazon Lex V2 bot\.  
Type: String  
Length Constraints: Minimum length of 20\. Maximum length of 2048\.  
Pattern: `^arn:[\w\-]+:iam::[\d]{12}:role/.+$`   
Required: Yes

## Response Syntax<a name="API_StartMigration_ResponseSyntax"></a>

```
HTTP/1.1 202
Content-type: application/json

{
   "migrationId": "string",
   "migrationStrategy": "string",
   "migrationTimestamp": number,
   "v1BotLocale": "string",
   "v1BotName": "string",
   "v1BotVersion": "string",
   "v2BotId": "string",
   "v2BotRole": "string"
}
```

## Response Elements<a name="API_StartMigration_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 202 response\.

The following data is returned in JSON format by the service\.

 ** [migrationId](#API_StartMigration_ResponseSyntax) **   <a name="lex-StartMigration-response-migrationId"></a>
The unique identifier that Amazon Lex assigned to the migration\.  
Type: String  
Length Constraints: Fixed length of 10\.  
Pattern: `^[0-9a-zA-Z]+$` 

 ** [migrationStrategy](#API_StartMigration_ResponseSyntax) **   <a name="lex-StartMigration-response-migrationStrategy"></a>
The strategy used to conduct the migration\.  
Type: String  
Valid Values:` CREATE_NEW | UPDATE_EXISTING` 

 ** [migrationTimestamp](#API_StartMigration_ResponseSyntax) **   <a name="lex-StartMigration-response-migrationTimestamp"></a>
The date and time that the migration started\.  
Type: Timestamp

 ** [v1BotLocale](#API_StartMigration_ResponseSyntax) **   <a name="lex-StartMigration-response-v1BotLocale"></a>
The locale used for the Amazon Lex V1 bot\.   
Type: String  
Valid Values:` de-DE | en-AU | en-GB | en-IN | en-US | es-419 | es-ES | es-US | fr-FR | fr-CA | it-IT | ja-JP` 

 ** [v1BotName](#API_StartMigration_ResponseSyntax) **   <a name="lex-StartMigration-response-v1BotName"></a>
The name of the Amazon Lex V1 bot that you are migrating to Amazon Lex V2\.  
Type: String  
Length Constraints: Minimum length of 2\. Maximum length of 50\.  
Pattern: `^([A-Za-z]_?)+$` 

 ** [v1BotVersion](#API_StartMigration_ResponseSyntax) **   <a name="lex-StartMigration-response-v1BotVersion"></a>
The version of the bot to migrate to Amazon Lex V2\.   
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 64\.  
Pattern: `\$LATEST|[0-9]+` 

 ** [v2BotId](#API_StartMigration_ResponseSyntax) **   <a name="lex-StartMigration-response-v2BotId"></a>
The unique identifier for the Amazon Lex V2 bot\.   
Type: String  
Length Constraints: Fixed length of 10\.  
Pattern: `^[0-9a-zA-Z]+$` 

 ** [v2BotRole](#API_StartMigration_ResponseSyntax) **   <a name="lex-StartMigration-response-v2BotRole"></a>
The IAM role that Amazon Lex uses to run the Amazon Lex V2 bot\.  
Type: String  
Length Constraints: Minimum length of 20\. Maximum length of 2048\.  
Pattern: `^arn:[\w\-]+:iam::[\d]{12}:role/.+$` 

## Errors<a name="API_StartMigration_Errors"></a>

 **AccessDeniedException**   
Your IAM user or role does not have permission to call the Amazon Lex V2 APIs required to migrate your bot\.  
HTTP Status Code: 403

 **BadRequestException**   
The request is not well formed\. For example, a value is invalid or a required field is missing\. Check the field values, and try again\.  
HTTP Status Code: 400

 **InternalFailureException**   
An internal Amazon Lex error occurred\. Try your request again\.  
HTTP Status Code: 500

 **LimitExceededException**   
The request exceeded a limit\. Try your request again\.  
HTTP Status Code: 429

 **NotFoundException**   
The resource specified in the request was not found\. Check the resource and try again\.  
HTTP Status Code: 404

## See Also<a name="API_StartMigration_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/lex-models-2017-04-19/StartMigration) 
+  [ AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/lex-models-2017-04-19/StartMigration) 
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/lex-models-2017-04-19/StartMigration) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/lex-models-2017-04-19/StartMigration) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/lex-models-2017-04-19/StartMigration) 
+  [ AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/lex-models-2017-04-19/StartMigration) 
+  [ AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/lex-models-2017-04-19/StartMigration) 
+  [ AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/lex-models-2017-04-19/StartMigration) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/lex-models-2017-04-19/StartMigration) 