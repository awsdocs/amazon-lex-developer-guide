# GetBots<a name="API_GetBots"></a>

Returns bot information as follows: 
+ If you provide the `nameContains` field, the response includes information for the `$LATEST` version of all bots whose name contains the specified string\.
+ If you don't specify the `nameContains` field, the operation returns information about the `$LATEST` version of all of your bots\.

This operation requires permission for the `lex:GetBots` action\.

## Request Syntax<a name="API_GetBots_RequestSyntax"></a>

```
GET /bots/?maxResults=maxResults&nameContains=nameContains&nextToken=nextToken HTTP/1.1
```

## URI Request Parameters<a name="API_GetBots_RequestParameters"></a>

The request uses the following URI parameters\.

 ** [maxResults](#API_GetBots_RequestSyntax) **   <a name="lex-GetBots-request-maxResults"></a>
The maximum number of bots to return in the response that the request will return\. The default is 10\.  
Valid Range: Minimum value of 1\. Maximum value of 50\.

 ** [nameContains](#API_GetBots_RequestSyntax) **   <a name="lex-GetBots-request-nameContains"></a>
Substring to match in bot names\. A bot will be returned if any part of its name matches the substring\. For example, "xyz" matches both "xyzabc" and "abcxyz\."  
Length Constraints: Minimum length of 2\. Maximum length of 50\.  
Pattern: `^([A-Za-z]_?)+$` 

 ** [nextToken](#API_GetBots_RequestSyntax) **   <a name="lex-GetBots-request-nextToken"></a>
A pagination token that fetches the next page of bots\. If the response to this call is truncated, Amazon Lex returns a pagination token in the response\. To fetch the next page of bots, specify the pagination token in the next request\. 

## Request Body<a name="API_GetBots_RequestBody"></a>

The request does not have a request body\.

## Response Syntax<a name="API_GetBots_ResponseSyntax"></a>

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

## Response Elements<a name="API_GetBots_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [bots](#API_GetBots_ResponseSyntax) **   <a name="lex-GetBots-response-bots"></a>
An array of `botMetadata` objects, with one entry for each bot\.   
Type: Array of [BotMetadata](API_BotMetadata.md) objects

 ** [nextToken](#API_GetBots_ResponseSyntax) **   <a name="lex-GetBots-response-nextToken"></a>
If the response is truncated, it includes a pagination token that you can specify in your next request to fetch the next page of bots\.   
Type: String

## Errors<a name="API_GetBots_Errors"></a>

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

## See Also<a name="API_GetBots_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/lex-models-2017-04-19/GetBots) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/lex-models-2017-04-19/GetBots) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/lex-models-2017-04-19/GetBots) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/lex-models-2017-04-19/GetBots) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/lex-models-2017-04-19/GetBots) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/lex-models-2017-04-19/GetBots) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/lex-models-2017-04-19/GetBots) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/lex-models-2017-04-19/GetBots) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/lex-models-2017-04-19/GetBots) 