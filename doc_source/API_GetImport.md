# GetImport<a name="API_GetImport"></a>

Gets information about an import job started with the `StartImport` operation\.

## Request Syntax<a name="API_GetImport_RequestSyntax"></a>

```
GET /imports/importId HTTP/1.1
```

## URI Request Parameters<a name="API_GetImport_RequestParameters"></a>

The request uses the following URI parameters\.

 ** [importId](#API_GetImport_RequestSyntax) **   <a name="lex-GetImport-request-importId"></a>
The identifier of the import job information to return\.  
Required: Yes

## Request Body<a name="API_GetImport_RequestBody"></a>

The request does not have a request body\.

## Response Syntax<a name="API_GetImport_ResponseSyntax"></a>

```
HTTP/1.1 200
Content-type: application/json

{
   "createdDate": number,
   "failureReason": [ "string" ],
   "importId": "string",
   "importStatus": "string",
   "mergeStrategy": "string",
   "name": "string",
   "resourceType": "string"
}
```

## Response Elements<a name="API_GetImport_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [createdDate](#API_GetImport_ResponseSyntax) **   <a name="lex-GetImport-response-createdDate"></a>
A timestamp for the date and time that the import job was created\.  
Type: Timestamp

 ** [failureReason](#API_GetImport_ResponseSyntax) **   <a name="lex-GetImport-response-failureReason"></a>
A string that describes why an import job failed to complete\.  
Type: Array of strings

 ** [importId](#API_GetImport_ResponseSyntax) **   <a name="lex-GetImport-response-importId"></a>
The identifier for the specific import job\.  
Type: String

 ** [importStatus](#API_GetImport_ResponseSyntax) **   <a name="lex-GetImport-response-importStatus"></a>
The status of the import job\. If the status is `FAILED`, you can get the reason for the failure from the `failureReason` field\.  
Type: String  
Valid Values:` IN_PROGRESS | COMPLETE | FAILED` 

 ** [mergeStrategy](#API_GetImport_ResponseSyntax) **   <a name="lex-GetImport-response-mergeStrategy"></a>
The action taken when there was a conflict between an existing resource and a resource in the import file\.  
Type: String  
Valid Values:` OVERWRITE_LATEST | FAIL_ON_CONFLICT` 

 ** [name](#API_GetImport_ResponseSyntax) **   <a name="lex-GetImport-response-name"></a>
The name given to the import job\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `[a-zA-Z_]+` 

 ** [resourceType](#API_GetImport_ResponseSyntax) **   <a name="lex-GetImport-response-resourceType"></a>
The type of resource imported\.  
Type: String  
Valid Values:` BOT | INTENT | SLOT_TYPE` 

## Errors<a name="API_GetImport_Errors"></a>

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

## See Also<a name="API_GetImport_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/lex-models-2017-04-19/GetImport) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/lex-models-2017-04-19/GetImport) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/lex-models-2017-04-19/GetImport) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/lex-models-2017-04-19/GetImport) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/lex-models-2017-04-19/GetImport) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/lex-models-2017-04-19/GetImport) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/lex-models-2017-04-19/GetImport) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/lex-models-2017-04-19/GetImport) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/lex-models-2017-04-19/GetImport) 