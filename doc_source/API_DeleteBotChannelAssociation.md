# DeleteBotChannelAssociation<a name="API_DeleteBotChannelAssociation"></a>

Deletes the association between an Amazon Lex bot and a messaging platform\.

This operation requires permission for the `lex:DeleteBotChannelAssociation` action\.

## Request Syntax<a name="API_DeleteBotChannelAssociation_RequestSyntax"></a>

```
DELETE /bots/botName/aliases/aliasName/channels/name HTTP/1.1
```

## URI Request Parameters<a name="API_DeleteBotChannelAssociation_RequestParameters"></a>

The request requires the following URI parameters\.

 ** botAlias **   
An alias that points to the specific version of the Amazon Lex bot to which this association is being made\.  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `^([A-Za-z]_?)+$` 

 ** botName **   
The name of the Amazon Lex bot\.  
Length Constraints: Minimum length of 2\. Maximum length of 50\.  
Pattern: `^([A-Za-z]_?)+$` 

 ** name **   
The name of the association\. The name is case sensitive\.   
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `^([A-Za-z]_?)+$` 

## Request Body<a name="API_DeleteBotChannelAssociation_RequestBody"></a>

The request does not have a request body\.

## Response Syntax<a name="API_DeleteBotChannelAssociation_ResponseSyntax"></a>

```
HTTP/1.1 204
```

## Response Elements<a name="API_DeleteBotChannelAssociation_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 204 response with an empty HTTP body\.

## Errors<a name="API_DeleteBotChannelAssociation_Errors"></a>

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

## See Also<a name="API_DeleteBotChannelAssociation_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:

+  [AWS Command Line Interface](http://docs.aws.amazon.com/goto/aws-cli/lex-models-2017-04-19/DeleteBotChannelAssociation) 

+  [AWS SDK for \.NET](http://docs.aws.amazon.com/goto/DotNetSDKV3/lex-models-2017-04-19/DeleteBotChannelAssociation) 

+  [AWS SDK for C\+\+](http://docs.aws.amazon.com/goto/SdkForCpp/lex-models-2017-04-19/DeleteBotChannelAssociation) 

+  [AWS SDK for Go](http://docs.aws.amazon.com/goto/SdkForGoV1/lex-models-2017-04-19/DeleteBotChannelAssociation) 

+  [AWS SDK for Java](http://docs.aws.amazon.com/goto/SdkForJava/lex-models-2017-04-19/DeleteBotChannelAssociation) 

+  [AWS SDK for JavaScript](http://docs.aws.amazon.com/goto/AWSJavaScriptSDK/lex-models-2017-04-19/DeleteBotChannelAssociation) 

+  [AWS SDK for PHP V3](http://docs.aws.amazon.com/goto/SdkForPHPV3/lex-models-2017-04-19/DeleteBotChannelAssociation) 

+  [AWS SDK for Python](http://docs.aws.amazon.com/goto/boto3/lex-models-2017-04-19/DeleteBotChannelAssociation) 

+  [AWS SDK for Ruby V2](http://docs.aws.amazon.com/goto/SdkForRubyV2/lex-models-2017-04-19/DeleteBotChannelAssociation) 