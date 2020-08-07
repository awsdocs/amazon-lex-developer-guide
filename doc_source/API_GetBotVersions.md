# GetBotVersions<a name="API_GetBotVersions"></a>

Gets information about all of the versions of a bot\.

The `GetBotVersions` operation returns a `BotMetadata` object for each version of a bot\. For example, if a bot has three numbered versions, the `GetBotVersions` operation returns four `BotMetadata` objects in the response, one for each numbered version and one for the `$LATEST` version\. 

The `GetBotVersions` operation always returns at least one version, the `$LATEST` version\.

This operation requires permissions for the `lex:GetBotVersions` action\.

## Request Syntax<a name="API_GetBotVersions_RequestSyntax"></a>

```
GET /bots/name/versions/?maxResults=maxResults&nextToken=nextToken HTTP/1.1
```

## URI Request Parameters<a name="API_GetBotVersions_RequestParameters"></a>

The request uses the following URI parameters\.

 ** [maxResults](#API_GetBotVersions_RequestSyntax) **   <a name="lex-GetBotVersions-request-maxResults"></a>
The maximum number of bot versions to return in the response\. The default is 10\.  
Valid Range: Minimum value of 1\. Maximum value of 50\.

 ** [name](#API_GetBotVersions_RequestSyntax) **   <a name="lex-GetBotVersions-request-name"></a>
The name of the bot for which versions should be returned\.  
Length Constraints: Minimum length of 2\. Maximum length of 50\.  
Pattern: `^([A-Za-z]_?)+$`   
Required: Yes

 ** [nextToken](#API_GetBotVersions_RequestSyntax) **   <a name="lex-GetBotVersions-request-nextToken"></a>
A pagination token for fetching the next page of bot versions\. If the response to this call is truncated, Amazon Lex returns a pagination token in the response\. To fetch the next page of versions, specify the pagination token in the next request\. 

## Request Body<a name="API_GetBotVersions_RequestBody"></a>

The request does not have a request body\.

## Response Syntax<a name="API_GetBotVersions_ResponseSyntax"></a>

```
HTTP/1.1 200
Content-type: application/json

{
   "bots": [ 
      { 
         "createdDate": number,
         "description": "string",
         "lastUpdatedDate": number,
         "name": "string",
         "status": "string",
         "version": "string"
      }
   ],
   "nextToken": "string"
}
```

## Response Elements<a name="API_GetBotVersions_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [bots](#API_GetBotVersions_ResponseSyntax) **   <a name="lex-GetBotVersions-response-bots"></a>
An array of `BotMetadata` objects, one for each numbered version of the bot plus one for the `$LATEST` version\.  
Type: Array of [BotMetadata](API_BotMetadata.md) objects

 ** [nextToken](#API_GetBotVersions_ResponseSyntax) **   <a name="lex-GetBotVersions-response-nextToken"></a>
A pagination token for fetching the next page of bot versions\. If the response to this call is truncated, Amazon Lex returns a pagination token in the response\. To fetch the next page of versions, specify the pagination token in the next request\.   
Type: String

## Errors<a name="API_GetBotVersions_Errors"></a>

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

## See Also<a name="API_GetBotVersions_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/lex-models-2017-04-19/GetBotVersions) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/lex-models-2017-04-19/GetBotVersions) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/lex-models-2017-04-19/GetBotVersions) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/lex-models-2017-04-19/GetBotVersions) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/lex-models-2017-04-19/GetBotVersions) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/lex-models-2017-04-19/GetBotVersions) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/lex-models-2017-04-19/GetBotVersions) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/lex-models-2017-04-19/GetBotVersions) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/lex-models-2017-04-19/GetBotVersions) 