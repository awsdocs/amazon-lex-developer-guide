# GetIntentVersions<a name="API_GetIntentVersions"></a>

Gets information about all of the versions of an intent\.

The `GetIntentVersions` operation returns an `IntentMetadata` object for each version of an intent\. For example, if an intent has three numbered versions, the `GetIntentVersions` operation returns four `IntentMetadata` objects in the response, one for each numbered version and one for the `$LATEST` version\. 

The `GetIntentVersions` operation always returns at least one version, the `$LATEST` version\.

This operation requires permissions for the `lex:GetIntentVersions` action\.

## Request Syntax<a name="API_GetIntentVersions_RequestSyntax"></a>

```
GET /intents/name/versions/?maxResults=maxResults&nextToken=nextToken HTTP/1.1
```

## URI Request Parameters<a name="API_GetIntentVersions_RequestParameters"></a>

The request requires the following URI parameters\.

 ** maxResults **   
The maximum number of intent versions to return in the response\. The default is 10\.  
Valid Range: Minimum value of 1\. Maximum value of 50\.

 ** name **   
The name of the intent for which versions should be returned\.  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `^([A-Za-z]_?)+$` 

 ** nextToken **   
A pagination token for fetching the next page of intent versions\. If the response to this call is truncated, Amazon Lex returns a pagination token in the response\. To fetch the next page of versions, specify the pagination token in the next request\. 

## Request Body<a name="API_GetIntentVersions_RequestBody"></a>

The request does not have a request body\.

## Response Syntax<a name="API_GetIntentVersions_ResponseSyntax"></a>

```
HTTP/1.1 200
Content-type: application/json

{
   "intents": [ 
      { 
         "createdDate": number,
         "description": "string",
         "lastUpdatedDate": number,
         "name": "string",
         "version": "string"
      }
   ],
   "nextToken": "string"
}
```

## Response Elements<a name="API_GetIntentVersions_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** intents **   
An array of `IntentMetadata` objects, one for each numbered version of the intent plus one for the `$LATEST` version\.  
Type: Array of [IntentMetadata](API_IntentMetadata.md) objects

 ** nextToken **   
A pagination token for fetching the next page of intent versions\. If the response to this call is truncated, Amazon Lex returns a pagination token in the response\. To fetch the next page of versions, specify the pagination token in the next request\.   
Type: String

## Errors<a name="API_GetIntentVersions_Errors"></a>

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

## See Also<a name="API_GetIntentVersions_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:

+  [AWS Command Line Interface](http://docs.aws.amazon.com/goto/aws-cli/lex-models-2017-04-19/GetIntentVersions) 

+  [AWS SDK for \.NET](http://docs.aws.amazon.com/goto/DotNetSDKV3/lex-models-2017-04-19/GetIntentVersions) 

+  [AWS SDK for C\+\+](http://docs.aws.amazon.com/goto/SdkForCpp/lex-models-2017-04-19/GetIntentVersions) 

+  [AWS SDK for Go](http://docs.aws.amazon.com/goto/SdkForGoV1/lex-models-2017-04-19/GetIntentVersions) 

+  [AWS SDK for Java](http://docs.aws.amazon.com/goto/SdkForJava/lex-models-2017-04-19/GetIntentVersions) 

+  [AWS SDK for JavaScript](http://docs.aws.amazon.com/goto/AWSJavaScriptSDK/lex-models-2017-04-19/GetIntentVersions) 

+  [AWS SDK for PHP V3](http://docs.aws.amazon.com/goto/SdkForPHPV3/lex-models-2017-04-19/GetIntentVersions) 

+  [AWS SDK for Python](http://docs.aws.amazon.com/goto/boto3/lex-models-2017-04-19/GetIntentVersions) 

+  [AWS SDK for Ruby V2](http://docs.aws.amazon.com/goto/SdkForRubyV2/lex-models-2017-04-19/GetIntentVersions) 