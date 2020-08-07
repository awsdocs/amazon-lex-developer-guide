# StartImport<a name="API_StartImport"></a>

Starts a job to import a resource to Amazon Lex\.

## Request Syntax<a name="API_StartImport_RequestSyntax"></a>

```
POST /imports/ HTTP/1.1
Content-type: application/json

{
   "mergeStrategy": "string",
   "payload": blob,
   "resourceType": "string",
   "tags": [ 
      { 
         "key": "string",
         "value": "string"
      }
   ]
}
```

## URI Request Parameters<a name="API_StartImport_RequestParameters"></a>

The request does not use any URI parameters\.

## Request Body<a name="API_StartImport_RequestBody"></a>

The request accepts the following data in JSON format\.

 ** [mergeStrategy](#API_StartImport_RequestSyntax) **   <a name="lex-StartImport-request-mergeStrategy"></a>
Specifies the action that the `StartImport` operation should take when there is an existing resource with the same name\.  
+ FAIL\_ON\_CONFLICT \- The import operation is stopped on the first conflict between a resource in the import file and an existing resource\. The name of the resource causing the conflict is in the `failureReason` field of the response to the `GetImport` operation\.

  OVERWRITE\_LATEST \- The import operation proceeds even if there is a conflict with an existing resource\. The $LASTEST version of the existing resource is overwritten with the data from the import file\.
Type: String  
Valid Values:` OVERWRITE_LATEST | FAIL_ON_CONFLICT`   
Required: Yes

 ** [payload](#API_StartImport_RequestSyntax) **   <a name="lex-StartImport-request-payload"></a>
A zip archive in binary format\. The archive should contain one file, a JSON file containing the resource to import\. The resource should match the type specified in the `resourceType` field\.  
Type: Base64\-encoded binary data object  
Required: Yes

 ** [resourceType](#API_StartImport_RequestSyntax) **   <a name="lex-StartImport-request-resourceType"></a>
Specifies the type of resource to export\. Each resource also exports any resources that it depends on\.   
+ A bot exports dependent intents\.
+ An intent exports dependent slot types\.
Type: String  
Valid Values:` BOT | INTENT | SLOT_TYPE`   
Required: Yes

 ** [tags](#API_StartImport_RequestSyntax) **   <a name="lex-StartImport-request-tags"></a>
A list of tags to add to the imported bot\. You can only add tags when you import a bot, you can't add tags to an intent or slot type\.  
Type: Array of [Tag](API_Tag.md) objects  
Array Members: Minimum number of 0 items\. Maximum number of 200 items\.  
Required: No

## Response Syntax<a name="API_StartImport_ResponseSyntax"></a>

```
HTTP/1.1 201
Content-type: application/json

{
   "createdDate": number,
   "importId": "string",
   "importStatus": "string",
   "mergeStrategy": "string",
   "name": "string",
   "resourceType": "string",
   "tags": [ 
      { 
         "key": "string",
         "value": "string"
      }
   ]
}
```

## Response Elements<a name="API_StartImport_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 201 response\.

The following data is returned in JSON format by the service\.

 ** [createdDate](#API_StartImport_ResponseSyntax) **   <a name="lex-StartImport-response-createdDate"></a>
A timestamp for the date and time that the import job was requested\.  
Type: Timestamp

 ** [importId](#API_StartImport_ResponseSyntax) **   <a name="lex-StartImport-response-importId"></a>
The identifier for the specific import job\.  
Type: String

 ** [importStatus](#API_StartImport_ResponseSyntax) **   <a name="lex-StartImport-response-importStatus"></a>
The status of the import job\. If the status is `FAILED`, you can get the reason for the failure using the `GetImport` operation\.  
Type: String  
Valid Values:` IN_PROGRESS | COMPLETE | FAILED` 

 ** [mergeStrategy](#API_StartImport_ResponseSyntax) **   <a name="lex-StartImport-response-mergeStrategy"></a>
The action to take when there is a merge conflict\.  
Type: String  
Valid Values:` OVERWRITE_LATEST | FAIL_ON_CONFLICT` 

 ** [name](#API_StartImport_ResponseSyntax) **   <a name="lex-StartImport-response-name"></a>
The name given to the import job\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `[a-zA-Z_]+` 

 ** [resourceType](#API_StartImport_ResponseSyntax) **   <a name="lex-StartImport-response-resourceType"></a>
The type of resource to import\.  
Type: String  
Valid Values:` BOT | INTENT | SLOT_TYPE` 

 ** [tags](#API_StartImport_ResponseSyntax) **   <a name="lex-StartImport-response-tags"></a>
A list of tags added to the imported bot\.  
Type: Array of [Tag](API_Tag.md) objects  
Array Members: Minimum number of 0 items\. Maximum number of 200 items\.

## Errors<a name="API_StartImport_Errors"></a>

 **BadRequestException**   
The request is not well formed\. For example, a value is invalid or a required field is missing\. Check the field values, and try again\.  
HTTP Status Code: 400

 **InternalFailureException**   
An internal Amazon Lex error occurred\. Try your request again\.  
HTTP Status Code: 500

 **LimitExceededException**   
The request exceeded a limit\. Try your request again\.  
HTTP Status Code: 429

## See Also<a name="API_StartImport_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/lex-models-2017-04-19/StartImport) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/lex-models-2017-04-19/StartImport) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/lex-models-2017-04-19/StartImport) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/lex-models-2017-04-19/StartImport) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/lex-models-2017-04-19/StartImport) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/lex-models-2017-04-19/StartImport) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/lex-models-2017-04-19/StartImport) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/lex-models-2017-04-19/StartImport) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/lex-models-2017-04-19/StartImport) 