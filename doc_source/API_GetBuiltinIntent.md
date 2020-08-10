# GetBuiltinIntent<a name="API_GetBuiltinIntent"></a>

Returns information about a built\-in intent\.

This operation requires permission for the `lex:GetBuiltinIntent` action\.

## Request Syntax<a name="API_GetBuiltinIntent_RequestSyntax"></a>

```
GET /builtins/intents/signature HTTP/1.1
```

## URI Request Parameters<a name="API_GetBuiltinIntent_RequestParameters"></a>

The request uses the following URI parameters\.

 ** [signature](#API_GetBuiltinIntent_RequestSyntax) **   <a name="lex-GetBuiltinIntent-request-signature"></a>
The unique identifier for a built\-in intent\. To find the signature for an intent, see [Standard Built\-in Intents](https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit/docs/built-in-intent-ref/standard-intents) in the *Alexa Skills Kit*\.  
Required: Yes

## Request Body<a name="API_GetBuiltinIntent_RequestBody"></a>

The request does not have a request body\.

## Response Syntax<a name="API_GetBuiltinIntent_ResponseSyntax"></a>

```
HTTP/1.1 200
Content-type: application/json

{
   "signature": "string",
   "slots": [ 
      { 
         "name": "string"
      }
   ],
   "supportedLocales": [ "string" ]
}
```

## Response Elements<a name="API_GetBuiltinIntent_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [signature](#API_GetBuiltinIntent_ResponseSyntax) **   <a name="lex-GetBuiltinIntent-response-signature"></a>
The unique identifier for a built\-in intent\.  
Type: String

 ** [slots](#API_GetBuiltinIntent_ResponseSyntax) **   <a name="lex-GetBuiltinIntent-response-slots"></a>
An array of `BuiltinIntentSlot` objects, one entry for each slot type in the intent\.  
Type: Array of [BuiltinIntentSlot](API_BuiltinIntentSlot.md) objects

 ** [supportedLocales](#API_GetBuiltinIntent_ResponseSyntax) **   <a name="lex-GetBuiltinIntent-response-supportedLocales"></a>
A list of locales that the intent supports\.  
Type: Array of strings  
Valid Values:` en-US | en-GB | de-DE` 

## Errors<a name="API_GetBuiltinIntent_Errors"></a>

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

## See Also<a name="API_GetBuiltinIntent_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/lex-models-2017-04-19/GetBuiltinIntent) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/lex-models-2017-04-19/GetBuiltinIntent) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/lex-models-2017-04-19/GetBuiltinIntent) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/lex-models-2017-04-19/GetBuiltinIntent) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/lex-models-2017-04-19/GetBuiltinIntent) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/lex-models-2017-04-19/GetBuiltinIntent) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/lex-models-2017-04-19/GetBuiltinIntent) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/lex-models-2017-04-19/GetBuiltinIntent) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/lex-models-2017-04-19/GetBuiltinIntent) 