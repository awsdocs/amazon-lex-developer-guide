# GetBuiltinIntents<a name="API_GetBuiltinIntents"></a>

Gets a list of built\-in intents that meet the specified criteria\.

This operation requires permission for the `lex:GetBuiltinIntents` action\.

## Request Syntax<a name="API_GetBuiltinIntents_RequestSyntax"></a>

```
GET /builtins/intents/?locale=locale&maxResults=maxResults&nextToken=nextToken&signatureContains=signatureContains HTTP/1.1
```

## URI Request Parameters<a name="API_GetBuiltinIntents_RequestParameters"></a>

The request uses the following URI parameters\.

 ** [locale](#API_GetBuiltinIntents_RequestSyntax) **   <a name="lex-GetBuiltinIntents-request-locale"></a>
A list of locales that the intent supports\.  
Valid Values:` en-US | en-GB | de-DE` 

 ** [maxResults](#API_GetBuiltinIntents_RequestSyntax) **   <a name="lex-GetBuiltinIntents-request-maxResults"></a>
The maximum number of intents to return in the response\. The default is 10\.  
Valid Range: Minimum value of 1\. Maximum value of 50\.

 ** [nextToken](#API_GetBuiltinIntents_RequestSyntax) **   <a name="lex-GetBuiltinIntents-request-nextToken"></a>
A pagination token that fetches the next page of intents\. If this API call is truncated, Amazon Lex returns a pagination token in the response\. To fetch the next page of intents, use the pagination token in the next request\.

 ** [signatureContains](#API_GetBuiltinIntents_RequestSyntax) **   <a name="lex-GetBuiltinIntents-request-signatureContains"></a>
Substring to match in built\-in intent signatures\. An intent will be returned if any part of its signature matches the substring\. For example, "xyz" matches both "xyzabc" and "abcxyz\." To find the signature for an intent, see [Standard Built\-in Intents](https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit/docs/built-in-intent-ref/standard-intents) in the *Alexa Skills Kit*\.

## Request Body<a name="API_GetBuiltinIntents_RequestBody"></a>

The request does not have a request body\.

## Response Syntax<a name="API_GetBuiltinIntents_ResponseSyntax"></a>

```
HTTP/1.1 200
Content-type: application/json

{
   "intents": [ 
      { 
         "signature": "string",
         "supportedLocales": [ "string" ]
      }
   ],
   "nextToken": "string"
}
```

## Response Elements<a name="API_GetBuiltinIntents_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [intents](#API_GetBuiltinIntents_ResponseSyntax) **   <a name="lex-GetBuiltinIntents-response-intents"></a>
An array of `builtinIntentMetadata` objects, one for each intent in the response\.  
Type: Array of [BuiltinIntentMetadata](API_BuiltinIntentMetadata.md) objects

 ** [nextToken](#API_GetBuiltinIntents_ResponseSyntax) **   <a name="lex-GetBuiltinIntents-response-nextToken"></a>
A pagination token that fetches the next page of intents\. If the response to this API call is truncated, Amazon Lex returns a pagination token in the response\. To fetch the next page of intents, specify the pagination token in the next request\.  
Type: String

## Errors<a name="API_GetBuiltinIntents_Errors"></a>

 **BadRequestException**   
The request is not well formed\. For example, a value is invalid or a required field is missing\. Check the field values, and try again\.  
HTTP Status Code: 400

 **InternalFailureException**   
An internal Amazon Lex error occurred\. Try your request again\.  
HTTP Status Code: 500

 **LimitExceededException**   
The request exceeded a limit\. Try your request again\.  
HTTP Status Code: 429

## See Also<a name="API_GetBuiltinIntents_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/lex-models-2017-04-19/GetBuiltinIntents) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/lex-models-2017-04-19/GetBuiltinIntents) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/lex-models-2017-04-19/GetBuiltinIntents) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/lex-models-2017-04-19/GetBuiltinIntents) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/lex-models-2017-04-19/GetBuiltinIntents) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/lex-models-2017-04-19/GetBuiltinIntents) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/lex-models-2017-04-19/GetBuiltinIntents) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/lex-models-2017-04-19/GetBuiltinIntents) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/lex-models-2017-04-19/GetBuiltinIntents) 