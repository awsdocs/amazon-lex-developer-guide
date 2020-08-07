# TagResource<a name="API_TagResource"></a>

Adds the specified tags to the specified resource\. If a tag key already exists, the existing value is replaced with the new value\.

## Request Syntax<a name="API_TagResource_RequestSyntax"></a>

```
POST /tags/resourceArn HTTP/1.1
Content-type: application/json

{
   "tags": [ 
      { 
         "key": "string",
         "value": "string"
      }
   ]
}
```

## URI Request Parameters<a name="API_TagResource_RequestParameters"></a>

The request uses the following URI parameters\.

 ** [resourceArn](#API_TagResource_RequestSyntax) **   <a name="lex-TagResource-request-resourceArn"></a>
The Amazon Resource Name \(ARN\) of the bot, bot alias, or bot channel to tag\.  
Length Constraints: Minimum length of 1\. Maximum length of 1011\.  
Required: Yes

## Request Body<a name="API_TagResource_RequestBody"></a>

The request accepts the following data in JSON format\.

 ** [tags](#API_TagResource_RequestSyntax) **   <a name="lex-TagResource-request-tags"></a>
A list of tag keys to add to the resource\. If a tag key already exists, the existing value is replaced with the new value\.  
Type: Array of [Tag](API_Tag.md) objects  
Array Members: Minimum number of 0 items\. Maximum number of 200 items\.  
Required: Yes

## Response Syntax<a name="API_TagResource_ResponseSyntax"></a>

```
HTTP/1.1 204
```

## Response Elements<a name="API_TagResource_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 204 response with an empty HTTP body\.

## Errors<a name="API_TagResource_Errors"></a>

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

## See Also<a name="API_TagResource_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/lex-models-2017-04-19/TagResource) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/lex-models-2017-04-19/TagResource) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/lex-models-2017-04-19/TagResource) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/lex-models-2017-04-19/TagResource) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/lex-models-2017-04-19/TagResource) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/lex-models-2017-04-19/TagResource) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/lex-models-2017-04-19/TagResource) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/lex-models-2017-04-19/TagResource) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/lex-models-2017-04-19/TagResource) 