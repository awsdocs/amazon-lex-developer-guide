# GetMigrations<a name="API_GetMigrations"></a>

Gets a list of migrations between Amazon Lex V1 and Amazon Lex V2\.

## Request Syntax<a name="API_GetMigrations_RequestSyntax"></a>

```
GET /migrations?maxResults=maxResults&migrationStatusEquals=migrationStatusEquals&nextToken=nextToken&sortByAttribute=sortByAttribute&sortByOrder=sortByOrder&v1BotNameContains=v1BotNameContains HTTP/1.1
```

## URI Request Parameters<a name="API_GetMigrations_RequestParameters"></a>

The request uses the following URI parameters\.

 ** [maxResults](#API_GetMigrations_RequestSyntax) **   <a name="lex-GetMigrations-request-maxResults"></a>
The maximum number of migrations to return in the response\. The default is 10\.  
Valid Range: Minimum value of 1\. Maximum value of 50\.

 ** [migrationStatusEquals](#API_GetMigrations_RequestSyntax) **   <a name="lex-GetMigrations-request-migrationStatusEquals"></a>
Filters the list to contain only migrations in the specified state\.  
Valid Values:` IN_PROGRESS | COMPLETED | FAILED` 

 ** [nextToken](#API_GetMigrations_RequestSyntax) **   <a name="lex-GetMigrations-request-nextToken"></a>
A pagination token that fetches the next page of migrations\. If the response to this operation is truncated, Amazon Lex returns a pagination token in the response\. To fetch the next page of migrations, specify the pagination token in the request\.

 ** [sortByAttribute](#API_GetMigrations_RequestSyntax) **   <a name="lex-GetMigrations-request-sortByAttribute"></a>
The field to sort the list of migrations by\. You can sort by the Amazon Lex V1 bot name or the date and time that the migration was started\.  
Valid Values:` V1_BOT_NAME | MIGRATION_DATE_TIME` 

 ** [sortByOrder](#API_GetMigrations_RequestSyntax) **   <a name="lex-GetMigrations-request-sortByOrder"></a>
The order so sort the list\.  
Valid Values:` ASCENDING | DESCENDING` 

 ** [v1BotNameContains](#API_GetMigrations_RequestSyntax) **   <a name="lex-GetMigrations-request-v1BotNameContains"></a>
Filters the list to contain only bots whose name contains the specified string\. The string is matched anywhere in the bot name\.  
Length Constraints: Minimum length of 2\. Maximum length of 50\.  
Pattern: `^([A-Za-z]_?)+$` 

## Request Body<a name="API_GetMigrations_RequestBody"></a>

The request does not have a request body\.

## Response Syntax<a name="API_GetMigrations_ResponseSyntax"></a>

```
HTTP/1.1 200
Content-type: application/json

{
   "migrationSummaries": [ 
      { 
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
   ],
   "nextToken": "string"
}
```

## Response Elements<a name="API_GetMigrations_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [migrationSummaries](#API_GetMigrations_ResponseSyntax) **   <a name="lex-GetMigrations-response-migrationSummaries"></a>
An array of summaries for migrations from Amazon Lex V1 to Amazon Lex V2\. To see details of the migration, use the `migrationId` from the summary in a call to the [GetMigration](API_GetMigration.md) operation\.  
Type: Array of [MigrationSummary](API_MigrationSummary.md) objects

 ** [nextToken](#API_GetMigrations_ResponseSyntax) **   <a name="lex-GetMigrations-response-nextToken"></a>
If the response is truncated, it includes a pagination token that you can specify in your next request to fetch the next page of migrations\.  
Type: String

## Errors<a name="API_GetMigrations_Errors"></a>

 **BadRequestException**   
The request is not well formed\. For example, a value is invalid or a required field is missing\. Check the field values, and try again\.  
HTTP Status Code: 400

 **InternalFailureException**   
An internal Amazon Lex error occurred\. Try your request again\.  
HTTP Status Code: 500

 **LimitExceededException**   
The request exceeded a limit\. Try your request again\.  
HTTP Status Code: 429

## See Also<a name="API_GetMigrations_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/lex-models-2017-04-19/GetMigrations) 
+  [ AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/lex-models-2017-04-19/GetMigrations) 
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/lex-models-2017-04-19/GetMigrations) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/lex-models-2017-04-19/GetMigrations) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/lex-models-2017-04-19/GetMigrations) 
+  [ AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/lex-models-2017-04-19/GetMigrations) 
+  [ AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/lex-models-2017-04-19/GetMigrations) 
+  [ AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/lex-models-2017-04-19/GetMigrations) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/lex-models-2017-04-19/GetMigrations) 