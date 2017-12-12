# GetExport<a name="API_GetExport"></a>

Exports the contents of a Amazon Lex resource in a specified format\. 

## Request Syntax<a name="API_GetExport_RequestSyntax"></a>

```
GET /exports/?exportType=exportType&name=name&resourceType=resourceType&version=version HTTP/1.1
```

## URI Request Parameters<a name="API_GetExport_RequestParameters"></a>

The request requires the following URI parameters\.

 ** exportType **   
The format of the exported data\.  
Valid Values:` ALEXA_SKILLS_KIT` 

 ** name **   
The name of the bot to export\.  
Length Constraints: Minimum length of 1\. Maximum length of 64\.  
Pattern: `[a-zA-Z_]+` 

 ** resourceType **   
The type of resource to export\.   
Valid Values:` BOT` 

 ** version **   
The version of the bot to export\.  
Length Constraints: Minimum length of 1\. Maximum length of 64\.  
Pattern: `[0-9]+` 

## Request Body<a name="API_GetExport_RequestBody"></a>

The request does not have a request body\.

## Response Syntax<a name="API_GetExport_ResponseSyntax"></a>

```
HTTP/1.1 200
Content-type: application/json

{
   "exportStatus": "string",
   "exportType": "string",
   "failureReason": "string",
   "name": "string",
   "resourceType": "string",
   "url": "string",
   "version": "string"
}
```

## Response Elements<a name="API_GetExport_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** exportStatus **   
The status of the export\.   

+  `IN_PROGRESS` \- The export is in progress\.

+  `READY` \- The export is complete\.

+  `FAILED` \- The export could not be completed\.
Type: String  
Valid Values:` IN_PROGRESS | READY | FAILED` 

 ** exportType **   
The format of the exported data\.  
Type: String  
Valid Values:` ALEXA_SKILLS_KIT` 

 ** failureReason **   
If `status` is `FAILED`, Amazon Lex provides the reason that it failed to export the resource\.  
Type: String

 ** name **   
The name of the bot being exported\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 64\.  
Pattern: `[a-zA-Z_]+` 

 ** resourceType **   
The type of the exported resource\.  
Type: String  
Valid Values:` BOT` 

 ** url **   
An S3 pre\-signed URL that provides the location of the exported resource\. The exported resource is a ZIP archive that contains the exported resource in JSON format\. The structure of the archive may change\. Your code should not rely on the archive structure\.  
Type: String

 ** version **   
The version of the bot being exported\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 64\.  
Pattern: `[0-9]+` 

## Errors<a name="API_GetExport_Errors"></a>

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

## See Also<a name="API_GetExport_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:

+  [AWS Command Line Interface](http://docs.aws.amazon.com/goto/aws-cli/lex-models-2017-04-19/GetExport) 

+  [AWS SDK for \.NET](http://docs.aws.amazon.com/goto/DotNetSDKV3/lex-models-2017-04-19/GetExport) 

+  [AWS SDK for C\+\+](http://docs.aws.amazon.com/goto/SdkForCpp/lex-models-2017-04-19/GetExport) 

+  [AWS SDK for Go](http://docs.aws.amazon.com/goto/SdkForGoV1/lex-models-2017-04-19/GetExport) 

+  [AWS SDK for Java](http://docs.aws.amazon.com/goto/SdkForJava/lex-models-2017-04-19/GetExport) 

+  [AWS SDK for JavaScript](http://docs.aws.amazon.com/goto/AWSJavaScriptSDK/lex-models-2017-04-19/GetExport) 

+  [AWS SDK for PHP V3](http://docs.aws.amazon.com/goto/SdkForPHPV3/lex-models-2017-04-19/GetExport) 

+  [AWS SDK for Python](http://docs.aws.amazon.com/goto/boto3/lex-models-2017-04-19/GetExport) 

+  [AWS SDK for Ruby V2](http://docs.aws.amazon.com/goto/SdkForRubyV2/lex-models-2017-04-19/GetExport) 