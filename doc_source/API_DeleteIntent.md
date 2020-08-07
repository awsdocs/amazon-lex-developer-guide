# DeleteIntent<a name="API_DeleteIntent"></a>

Deletes all versions of the intent, including the `$LATEST` version\. To delete a specific version of the intent, use the [DeleteIntentVersion](API_DeleteIntentVersion.md) operation\.

 You can delete a version of an intent only if it is not referenced\. To delete an intent that is referred to in one or more bots \(see [Amazon Lex: How It Works](how-it-works.md)\), you must remove those references first\. 

**Note**  
 If you get the `ResourceInUseException` exception, it provides an example reference that shows where the intent is referenced\. To remove the reference to the intent, either update the bot or delete it\. If you get the same exception when you attempt to delete the intent again, repeat until the intent has no references and the call to `DeleteIntent` is successful\. 

 This operation requires permission for the `lex:DeleteIntent` action\. 

## Request Syntax<a name="API_DeleteIntent_RequestSyntax"></a>

```
DELETE /intents/name HTTP/1.1
```

## URI Request Parameters<a name="API_DeleteIntent_RequestParameters"></a>

The request uses the following URI parameters\.

 ** [name](#API_DeleteIntent_RequestSyntax) **   <a name="lex-DeleteIntent-request-name"></a>
The name of the intent\. The name is case sensitive\.   
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `^([A-Za-z]_?)+$`   
Required: Yes

## Request Body<a name="API_DeleteIntent_RequestBody"></a>

The request does not have a request body\.

## Response Syntax<a name="API_DeleteIntent_ResponseSyntax"></a>

```
HTTP/1.1 204
```

## Response Elements<a name="API_DeleteIntent_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 204 response with an empty HTTP body\.

## Errors<a name="API_DeleteIntent_Errors"></a>

 **BadRequestException**   
The request is not well formed\. For example, a value is invalid or a required field is missing\. Check the field values, and try again\.  
HTTP Status Code: 400

 **ConflictException**   
 There was a conflict processing the request\. Try your request again\.   
HTTP Status Code: 409

 **InternalFailureException**   
An internal Amazon Lex error occurred\. Try your request again\.  
HTTP Status Code: 500

 **LimitExceededException**   
The request exceeded a limit\. Try your request again\.  
HTTP Status Code: 429

 **NotFoundException**   
The resource specified in the request was not found\. Check the resource and try again\.  
HTTP Status Code: 404

 **ResourceInUseException**   
The resource that you are attempting to delete is referred to by another resource\. Use this information to remove references to the resource that you are trying to delete\.  
The body of the exception contains a JSON object that describes the resource\.  
 `{ "resourceType": BOT | BOTALIAS | BOTCHANNEL | INTENT,`   
 `"resourceReference": {`   
 `"name": string, "version": string } }`   
HTTP Status Code: 400

## See Also<a name="API_DeleteIntent_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/lex-models-2017-04-19/DeleteIntent) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/lex-models-2017-04-19/DeleteIntent) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/lex-models-2017-04-19/DeleteIntent) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/lex-models-2017-04-19/DeleteIntent) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/lex-models-2017-04-19/DeleteIntent) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/lex-models-2017-04-19/DeleteIntent) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/lex-models-2017-04-19/DeleteIntent) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/lex-models-2017-04-19/DeleteIntent) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/lex-models-2017-04-19/DeleteIntent) 