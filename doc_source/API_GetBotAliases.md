# GetBotAliases<a name="API_GetBotAliases"></a>

Returns a list of aliases for a specified Amazon Lex bot\.

This operation requires permissions for the `lex:GetBotAliases` action\.

## Request Syntax<a name="API_GetBotAliases_RequestSyntax"></a>

```
GET /bots/botName/aliases/?maxResults=maxResults&nameContains=nameContains&nextToken=nextToken HTTP/1.1
```

## URI Request Parameters<a name="API_GetBotAliases_RequestParameters"></a>

The request uses the following URI parameters\.

 ** [botName](#API_GetBotAliases_RequestSyntax) **   <a name="lex-GetBotAliases-request-botName"></a>
The name of the bot\.  
Length Constraints: Minimum length of 2\. Maximum length of 50\.  
Pattern: `^([A-Za-z]_?)+$`   
Required: Yes

 ** [maxResults](#API_GetBotAliases_RequestSyntax) **   <a name="lex-GetBotAliases-request-maxResults"></a>
The maximum number of aliases to return in the response\. The default is 50\. \.   
Valid Range: Minimum value of 1\. Maximum value of 50\.

 ** [nameContains](#API_GetBotAliases_RequestSyntax) **   <a name="lex-GetBotAliases-request-nameContains"></a>
Substring to match in bot alias names\. An alias will be returned if any part of its name matches the substring\. For example, "xyz" matches both "xyzabc" and "abcxyz\."  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `^([A-Za-z]_?)+$` 

 ** [nextToken](#API_GetBotAliases_RequestSyntax) **   <a name="lex-GetBotAliases-request-nextToken"></a>
A pagination token for fetching the next page of aliases\. If the response to this call is truncated, Amazon Lex returns a pagination token in the response\. To fetch the next page of aliases, specify the pagination token in the next request\. 

## Request Body<a name="API_GetBotAliases_RequestBody"></a>

The request does not have a request body\.

## Response Syntax<a name="API_GetBotAliases_ResponseSyntax"></a>

```
HTTP/1.1 200
Content-type: application/json

{
   "BotAliases": [ 
      { 
         "botName": "string",
         "botVersion": "string",
         "checksum": "string",
         "conversationLogs": { 
            "iamRoleArn": "string",
            "logSettings": [ 
               { 
                  "destination": "string",
                  "kmsKeyArn": "string",
                  "logType": "string",
                  "resourceArn": "string",
                  "resourcePrefix": "string"
               }
            ]
         },
         "createdDate": number,
         "description": "string",
         "lastUpdatedDate": number,
         "name": "string"
      }
   ],
   "nextToken": "string"
}
```

## Response Elements<a name="API_GetBotAliases_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [BotAliases](#API_GetBotAliases_ResponseSyntax) **   <a name="lex-GetBotAliases-response-BotAliases"></a>
An array of `BotAliasMetadata` objects, each describing a bot alias\.  
Type: Array of [BotAliasMetadata](API_BotAliasMetadata.md) objects

 ** [nextToken](#API_GetBotAliases_ResponseSyntax) **   <a name="lex-GetBotAliases-response-nextToken"></a>
A pagination token for fetching next page of aliases\. If the response to this call is truncated, Amazon Lex returns a pagination token in the response\. To fetch the next page of aliases, specify the pagination token in the next request\.   
Type: String

## Errors<a name="API_GetBotAliases_Errors"></a>

 **BadRequestException**   
The request is not well formed\. For example, a value is invalid or a required field is missing\. Check the field values, and try again\.  
HTTP Status Code: 400

 **InternalFailureException**   
An internal Amazon Lex error occurred\. Try your request again\.  
HTTP Status Code: 500

 **LimitExceededException**   
The request exceeded a limit\. Try your request again\.  
HTTP Status Code: 429

## See Also<a name="API_GetBotAliases_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/lex-models-2017-04-19/GetBotAliases) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/lex-models-2017-04-19/GetBotAliases) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/lex-models-2017-04-19/GetBotAliases) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/lex-models-2017-04-19/GetBotAliases) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/lex-models-2017-04-19/GetBotAliases) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/lex-models-2017-04-19/GetBotAliases) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/lex-models-2017-04-19/GetBotAliases) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/lex-models-2017-04-19/GetBotAliases) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/lex-models-2017-04-19/GetBotAliases) 