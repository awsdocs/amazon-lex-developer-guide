# GetBuiltinSlotTypes<a name="API_GetBuiltinSlotTypes"></a>

Gets a list of built\-in slot types that meet the specified criteria\.

For a list of built\-in slot types, see [Slot Type Reference](https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit/docs/built-in-intent-ref/slot-type-reference) in the *Alexa Skills Kit*\.

This operation requires permission for the `lex:GetBuiltInSlotTypes` action\.

## Request Syntax<a name="API_GetBuiltinSlotTypes_RequestSyntax"></a>

```
GET /builtins/slottypes/?locale=locale&maxResults=maxResults&nextToken=nextToken&signatureContains=signatureContains HTTP/1.1
```

## URI Request Parameters<a name="API_GetBuiltinSlotTypes_RequestParameters"></a>

The request uses the following URI parameters\.

 ** [locale](#API_GetBuiltinSlotTypes_RequestSyntax) **   <a name="lex-GetBuiltinSlotTypes-request-locale"></a>
A list of locales that the slot type supports\.  
Valid Values:` en-US | en-GB | de-DE` 

 ** [maxResults](#API_GetBuiltinSlotTypes_RequestSyntax) **   <a name="lex-GetBuiltinSlotTypes-request-maxResults"></a>
The maximum number of slot types to return in the response\. The default is 10\.  
Valid Range: Minimum value of 1\. Maximum value of 50\.

 ** [nextToken](#API_GetBuiltinSlotTypes_RequestSyntax) **   <a name="lex-GetBuiltinSlotTypes-request-nextToken"></a>
A pagination token that fetches the next page of slot types\. If the response to this API call is truncated, Amazon Lex returns a pagination token in the response\. To fetch the next page of slot types, specify the pagination token in the next request\.

 ** [signatureContains](#API_GetBuiltinSlotTypes_RequestSyntax) **   <a name="lex-GetBuiltinSlotTypes-request-signatureContains"></a>
Substring to match in built\-in slot type signatures\. A slot type will be returned if any part of its signature matches the substring\. For example, "xyz" matches both "xyzabc" and "abcxyz\."

## Request Body<a name="API_GetBuiltinSlotTypes_RequestBody"></a>

The request does not have a request body\.

## Response Syntax<a name="API_GetBuiltinSlotTypes_ResponseSyntax"></a>

```
HTTP/1.1 200
Content-type: application/json

{
   "nextToken": "string",
   "slotTypes": [ 
      { 
         "signature": "string",
         "supportedLocales": [ "string" ]
      }
   ]
}
```

## Response Elements<a name="API_GetBuiltinSlotTypes_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [nextToken](#API_GetBuiltinSlotTypes_ResponseSyntax) **   <a name="lex-GetBuiltinSlotTypes-response-nextToken"></a>
If the response is truncated, the response includes a pagination token that you can use in your next request to fetch the next page of slot types\.  
Type: String

 ** [slotTypes](#API_GetBuiltinSlotTypes_ResponseSyntax) **   <a name="lex-GetBuiltinSlotTypes-response-slotTypes"></a>
An array of `BuiltInSlotTypeMetadata` objects, one entry for each slot type returned\.  
Type: Array of [BuiltinSlotTypeMetadata](API_BuiltinSlotTypeMetadata.md) objects

## Errors<a name="API_GetBuiltinSlotTypes_Errors"></a>

 **BadRequestException**   
The request is not well formed\. For example, a value is invalid or a required field is missing\. Check the field values, and try again\.  
HTTP Status Code: 400

 **InternalFailureException**   
An internal Amazon Lex error occurred\. Try your request again\.  
HTTP Status Code: 500

 **LimitExceededException**   
The request exceeded a limit\. Try your request again\.  
HTTP Status Code: 429

## See Also<a name="API_GetBuiltinSlotTypes_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/lex-models-2017-04-19/GetBuiltinSlotTypes) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/lex-models-2017-04-19/GetBuiltinSlotTypes) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/lex-models-2017-04-19/GetBuiltinSlotTypes) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/lex-models-2017-04-19/GetBuiltinSlotTypes) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/lex-models-2017-04-19/GetBuiltinSlotTypes) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/lex-models-2017-04-19/GetBuiltinSlotTypes) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/lex-models-2017-04-19/GetBuiltinSlotTypes) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/lex-models-2017-04-19/GetBuiltinSlotTypes) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/lex-models-2017-04-19/GetBuiltinSlotTypes) 