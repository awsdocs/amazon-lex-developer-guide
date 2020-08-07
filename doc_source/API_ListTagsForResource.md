# ListTagsForResource<a name="API_ListTagsForResource"></a>

Gets a list of tags associated with the specified resource\. Only bots, bot aliases, and bot channels can have tags associated with them\.

## Request Syntax<a name="API_ListTagsForResource_RequestSyntax"></a>

```
GET /tags/resourceArn HTTP/1.1
```

## URI Request Parameters<a name="API_ListTagsForResource_RequestParameters"></a>

The request uses the following URI parameters\.

 ** [resourceArn](#API_ListTagsForResource_RequestSyntax) **   <a name="lex-ListTagsForResource-request-resourceArn"></a>
The Amazon Resource Name \(ARN\) of the resource to get a list of tags for\.  
Length Constraints: Minimum length of 1\. Maximum length of 1011\.  
Required: Yes

## Request Body<a name="API_ListTagsForResource_RequestBody"></a>

The request does not have a request body\.

## Response Syntax<a name="API_ListTagsForResource_ResponseSyntax"></a>

```
HTTP/1.1 200
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

## Response Elements<a name="API_ListTagsForResource_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [tags](#API_ListTagsForResource_ResponseSyntax) **   <a name="lex-ListTagsForResource-response-tags"></a>
The tags associated with a resource\.  
Type: Array of [Tag](API_Tag.md) objects  
Array Members: Minimum number of 0 items\. Maximum number of 200 items\.

## Errors<a name="API_ListTagsForResource_Errors"></a>

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

## See Also<a name="API_ListTagsForResource_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/lex-models-2017-04-19/ListTagsForResource) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/lex-models-2017-04-19/ListTagsForResource) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/lex-models-2017-04-19/ListTagsForResource) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/lex-models-2017-04-19/ListTagsForResource) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/lex-models-2017-04-19/ListTagsForResource) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/lex-models-2017-04-19/ListTagsForResource) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/lex-models-2017-04-19/ListTagsForResource) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/lex-models-2017-04-19/ListTagsForResource) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/lex-models-2017-04-19/ListTagsForResource) 