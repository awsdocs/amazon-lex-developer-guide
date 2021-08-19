# GetMigration<a name="API_GetMigration"></a>

Provides details about an ongoing or complete migration from an Amazon Lex V1 bot to an Amazon Lex V2 bot\. Use this operation to view the migration alerts and warnings related to the migration\.

## Request Syntax<a name="API_GetMigration_RequestSyntax"></a>

```
GET /migrations/migrationId HTTP/1.1
```

## URI Request Parameters<a name="API_GetMigration_RequestParameters"></a>

The request uses the following URI parameters\.

 ** [migrationId](#API_GetMigration_RequestSyntax) **   <a name="lex-GetMigration-request-migrationId"></a>
The unique identifier of the migration to view\. The `migrationID` is returned by the [StartMigration](API_StartMigration.md) operation\.  
Length Constraints: Fixed length of 10\.  
Pattern: `^[0-9a-zA-Z]+$`   
Required: Yes

## Request Body<a name="API_GetMigration_RequestBody"></a>

The request does not have a request body\.

## Response Syntax<a name="API_GetMigration_ResponseSyntax"></a>

```
HTTP/1.1 200
Content-type: application/json

{
   "alerts": [ 
      { 
         "details": [ "string" ],
         "message": "string",
         "referenceURLs": [ "string" ],
         "type": "string"
      }
   ],
   "migrationId": "string",
   "migrationStatus": "string",
   "migrationStrategy": "string",
   "migrationTimestamp": number,
   "v1BotLocale": "string",
   "v1BotName": "string",
   "v1BotVersion": "string",
   "v2BotId": "string",
   "v2BotRole": "string"
}
```

## Response Elements<a name="API_GetMigration_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [alerts](#API_GetMigration_ResponseSyntax) **   <a name="lex-GetMigration-response-alerts"></a>
A list of alerts and warnings that indicate issues with the migration for the Amazon Lex V1 bot to Amazon Lex V2\. You receive a warning when an Amazon Lex V1 feature has a different implementation in Amazon Lex V2\.  
For more information, see [Migrating a bot](https://docs.aws.amazon.com/lexv2/latest/dg/migrate.html) in the *Amazon Lex V2 developer guide*\.  
Type: Array of [MigrationAlert](API_MigrationAlert.md) objects

 ** [migrationId](#API_GetMigration_ResponseSyntax) **   <a name="lex-GetMigration-response-migrationId"></a>
The unique identifier of the migration\. This is the same as the identifier used when calling the `GetMigration` operation\.  
Type: String  
Length Constraints: Fixed length of 10\.  
Pattern: `^[0-9a-zA-Z]+$` 

 ** [migrationStatus](#API_GetMigration_ResponseSyntax) **   <a name="lex-GetMigration-response-migrationStatus"></a>
Indicates the status of the migration\. When the status is `COMPLETE` the migration is finished and the bot is available in Amazon Lex V2\. There may be alerts and warnings that need to be resolved to complete the migration\.  
Type: String  
Valid Values:` IN_PROGRESS | COMPLETED | FAILED` 

 ** [migrationStrategy](#API_GetMigration_ResponseSyntax) **   <a name="lex-GetMigration-response-migrationStrategy"></a>
The strategy used to conduct the migration\.  
+  `CREATE_NEW` \- Creates a new Amazon Lex V2 bot and migrates the Amazon Lex V1 bot to the new bot\.
+  `UPDATE_EXISTING` \- Overwrites the existing Amazon Lex V2 bot metadata and the locale being migrated\. It doesn't change any other locales in the Amazon Lex V2 bot\. If the locale doesn't exist, a new locale is created in the Amazon Lex V2 bot\.
Type: String  
Valid Values:` CREATE_NEW | UPDATE_EXISTING` 

 ** [migrationTimestamp](#API_GetMigration_ResponseSyntax) **   <a name="lex-GetMigration-response-migrationTimestamp"></a>
The date and time that the migration started\.  
Type: Timestamp

 ** [v1BotLocale](#API_GetMigration_ResponseSyntax) **   <a name="lex-GetMigration-response-v1BotLocale"></a>
The locale of the Amazon Lex V1 bot migrated to Amazon Lex V2\.  
Type: String  
Valid Values:` de-DE | en-AU | en-GB | en-IN | en-US | es-419 | es-ES | es-US | fr-FR | fr-CA | it-IT | ja-JP` 

 ** [v1BotName](#API_GetMigration_ResponseSyntax) **   <a name="lex-GetMigration-response-v1BotName"></a>
The name of the Amazon Lex V1 bot migrated to Amazon Lex V2\.  
Type: String  
Length Constraints: Minimum length of 2\. Maximum length of 50\.  
Pattern: `^([A-Za-z]_?)+$` 

 ** [v1BotVersion](#API_GetMigration_ResponseSyntax) **   <a name="lex-GetMigration-response-v1BotVersion"></a>
The version of the Amazon Lex V1 bot migrated to Amazon Lex V2\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 64\.  
Pattern: `\$LATEST|[0-9]+` 

 ** [v2BotId](#API_GetMigration_ResponseSyntax) **   <a name="lex-GetMigration-response-v2BotId"></a>
The unique identifier of the Amazon Lex V2 bot that the Amazon Lex V1 is being migrated to\.  
Type: String  
Length Constraints: Fixed length of 10\.  
Pattern: `^[0-9a-zA-Z]+$` 

 ** [v2BotRole](#API_GetMigration_ResponseSyntax) **   <a name="lex-GetMigration-response-v2BotRole"></a>
The IAM role that Amazon Lex uses to run the Amazon Lex V2 bot\.  
Type: String  
Length Constraints: Minimum length of 20\. Maximum length of 2048\.  
Pattern: `^arn:[\w\-]+:iam::[\d]{12}:role/.+$` 

## Errors<a name="API_GetMigration_Errors"></a>

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

## See Also<a name="API_GetMigration_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/lex-models-2017-04-19/GetMigration) 
+  [ AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/lex-models-2017-04-19/GetMigration) 
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/lex-models-2017-04-19/GetMigration) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/lex-models-2017-04-19/GetMigration) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/lex-models-2017-04-19/GetMigration) 
+  [ AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/lex-models-2017-04-19/GetMigration) 
+  [ AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/lex-models-2017-04-19/GetMigration) 
+  [ AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/lex-models-2017-04-19/GetMigration) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/lex-models-2017-04-19/GetMigration) 