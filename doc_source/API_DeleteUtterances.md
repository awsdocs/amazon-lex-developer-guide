# DeleteUtterances<a name="API_DeleteUtterances"></a>

Deletes stored utterances\.

Amazon Lex stores the utterances that users send to your bot\. Utterances are stored for 15 days for use with the [GetUtterancesView](API_GetUtterancesView.md) operation, and then stored indefinitely for use in improving the ability of your bot to respond to user input\.

Use the `DeleteUtterances` operation to manually delete stored utterances for a specific user\. When you use the `DeleteUtterances` operation, utterances stored for improving your bot's ability to respond to user input are deleted immediately\. Utterances stored for use with the `GetUtterancesView` operation are deleted after 15 days\.

This operation requires permissions for the `lex:DeleteUtterances` action\.

## Request Syntax<a name="API_DeleteUtterances_RequestSyntax"></a>

```
DELETE /bots/botName/utterances/userId HTTP/1.1
```

## URI Request Parameters<a name="API_DeleteUtterances_RequestParameters"></a>

The request uses the following URI parameters\.

 ** [botName](#API_DeleteUtterances_RequestSyntax) **   <a name="lex-DeleteUtterances-request-botName"></a>
The name of the bot that stored the utterances\.  
Length Constraints: Minimum length of 2\. Maximum length of 50\.  
Pattern: `^([A-Za-z]_?)+$`   
Required: Yes

 ** [userId](#API_DeleteUtterances_RequestSyntax) **   <a name="lex-DeleteUtterances-request-userId"></a>
 The unique identifier for the user that made the utterances\. This is the user ID that was sent in the [PostContent](http://docs.aws.amazon.com/lex/latest/dg/API_runtime_PostContent.html) or [PostText](http://docs.aws.amazon.com/lex/latest/dg/API_runtime_PostText.html) operation request that contained the utterance\.  
Length Constraints: Minimum length of 2\. Maximum length of 100\.  
Required: Yes

## Request Body<a name="API_DeleteUtterances_RequestBody"></a>

The request does not have a request body\.

## Response Syntax<a name="API_DeleteUtterances_ResponseSyntax"></a>

```
HTTP/1.1 204
```

## Response Elements<a name="API_DeleteUtterances_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 204 response with an empty HTTP body\.

## Errors<a name="API_DeleteUtterances_Errors"></a>

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

## See Also<a name="API_DeleteUtterances_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/lex-models-2017-04-19/DeleteUtterances) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/lex-models-2017-04-19/DeleteUtterances) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/lex-models-2017-04-19/DeleteUtterances) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/lex-models-2017-04-19/DeleteUtterances) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/lex-models-2017-04-19/DeleteUtterances) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/lex-models-2017-04-19/DeleteUtterances) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/lex-models-2017-04-19/DeleteUtterances) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/lex-models-2017-04-19/DeleteUtterances) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/lex-models-2017-04-19/DeleteUtterances) 