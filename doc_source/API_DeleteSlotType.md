# DeleteSlotType<a name="API_DeleteSlotType"></a>

Deletes all versions of the slot type, including the `$LATEST` version\. To delete a specific version of the slot type, use the [DeleteSlotTypeVersion](API_DeleteSlotTypeVersion.md) operation\.

 You can delete a version of a slot type only if it is not referenced\. To delete a slot type that is referred to in one or more intents, you must remove those references first\. 

**Note**  
 If you get the `ResourceInUseException` exception, the exception provides an example reference that shows the intent where the slot type is referenced\. To remove the reference to the slot type, either update the intent or delete it\. If you get the same exception when you attempt to delete the slot type again, repeat until the slot type has no references and the `DeleteSlotType` call is successful\. 

This operation requires permission for the `lex:DeleteSlotType` action\.

## Request Syntax<a name="API_DeleteSlotType_RequestSyntax"></a>

```
DELETE /slottypes/name HTTP/1.1
```

## URI Request Parameters<a name="API_DeleteSlotType_RequestParameters"></a>

The request uses the following URI parameters\.

 ** [name](#API_DeleteSlotType_RequestSyntax) **   <a name="lex-DeleteSlotType-request-name"></a>
The name of the slot type\. The name is case sensitive\.   
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `^([A-Za-z]_?)+$`   
Required: Yes

## Request Body<a name="API_DeleteSlotType_RequestBody"></a>

The request does not have a request body\.

## Response Syntax<a name="API_DeleteSlotType_ResponseSyntax"></a>

```
HTTP/1.1 204
```

## Response Elements<a name="API_DeleteSlotType_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 204 response with an empty HTTP body\.

## Errors<a name="API_DeleteSlotType_Errors"></a>

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

## See Also<a name="API_DeleteSlotType_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/lex-models-2017-04-19/DeleteSlotType) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/lex-models-2017-04-19/DeleteSlotType) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/lex-models-2017-04-19/DeleteSlotType) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/lex-models-2017-04-19/DeleteSlotType) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/lex-models-2017-04-19/DeleteSlotType) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/lex-models-2017-04-19/DeleteSlotType) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/lex-models-2017-04-19/DeleteSlotType) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/lex-models-2017-04-19/DeleteSlotType) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/lex-models-2017-04-19/DeleteSlotType) 