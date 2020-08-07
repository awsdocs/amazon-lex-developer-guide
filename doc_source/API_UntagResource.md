# UntagResource<a name="API_UntagResource"></a>

Removes tags from a bot, bot alias or bot channel\.

## Request Syntax<a name="API_UntagResource_RequestSyntax"></a>

```
DELETE /tags/resourceArn?tagKeys=tagKeys HTTP/1.1
```

## URI Request Parameters<a name="API_UntagResource_RequestParameters"></a>

The request uses the following URI parameters\.

 ** [resourceArn](#API_UntagResource_RequestSyntax) **   <a name="lex-UntagResource-request-resourceArn"></a>
The Amazon Resource Name \(ARN\) of the resource to remove the tags from\.  
Length Constraints: Minimum length of 1\. Maximum length of 1011\.  
Required: Yes

 ** [tagKeys](#API_UntagResource_RequestSyntax) **   <a name="lex-UntagResource-request-tagKeys"></a>
A list of tag keys to remove from the resource\. If a tag key does not exist on the resource, it is ignored\.  
Array Members: Minimum number of 0 items\. Maximum number of 200 items\.  
Length Constraints: Minimum length of 1\. Maximum length of 128\.  
Required: Yes

## Request Body<a name="API_UntagResource_RequestBody"></a>

The request does not have a request body\.

## Response Syntax<a name="API_UntagResource_ResponseSyntax"></a>

```
HTTP/1.1 204
```

## Response Elements<a name="API_UntagResource_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 204 response with an empty HTTP body\.

## Errors<a name="API_UntagResource_Errors"></a>

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

## See Also<a name="API_UntagResource_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/lex-models-2017-04-19/UntagResource) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/lex-models-2017-04-19/UntagResource) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/lex-models-2017-04-19/UntagResource) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/lex-models-2017-04-19/UntagResource) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/lex-models-2017-04-19/UntagResource) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/lex-models-2017-04-19/UntagResource) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/lex-models-2017-04-19/UntagResource) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/lex-models-2017-04-19/UntagResource) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/lex-models-2017-04-19/UntagResource) 