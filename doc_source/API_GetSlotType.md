# GetSlotType<a name="API_GetSlotType"></a>

Returns information about a specific version of a slot type\. In addition to specifying the slot type name, you must specify the slot type version\.

This operation requires permissions for the `lex:GetSlotType` action\.

## Request Syntax<a name="API_GetSlotType_RequestSyntax"></a>

```
GET /slottypes/name/versions/version HTTP/1.1
```

## URI Request Parameters<a name="API_GetSlotType_RequestParameters"></a>

The request uses the following URI parameters\.

 ** [name](#API_GetSlotType_RequestSyntax) **   <a name="lex-GetSlotType-request-name"></a>
The name of the slot type\. The name is case sensitive\.   
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `^([A-Za-z]_?)+$`   
Required: Yes

 ** [version](#API_GetSlotType_RequestSyntax) **   <a name="lex-GetSlotType-request-version"></a>
The version of the slot type\.   
Length Constraints: Minimum length of 1\. Maximum length of 64\.  
Pattern: `\$LATEST|[0-9]+`   
Required: Yes

## Request Body<a name="API_GetSlotType_RequestBody"></a>

The request does not have a request body\.

## Response Syntax<a name="API_GetSlotType_ResponseSyntax"></a>

```
HTTP/1.1 200
Content-type: application/json

{
   "checksum": "string",
   "createdDate": number,
   "description": "string",
   "enumerationValues": [ 
      { 
         "synonyms": [ "string" ],
         "value": "string"
      }
   ],
   "lastUpdatedDate": number,
   "name": "string",
   "parentSlotTypeSignature": "string",
   "slotTypeConfigurations": [ 
      { 
         "regexConfiguration": { 
            "pattern": "string"
         }
      }
   ],
   "valueSelectionStrategy": "string",
   "version": "string"
}
```

## Response Elements<a name="API_GetSlotType_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [checksum](#API_GetSlotType_ResponseSyntax) **   <a name="lex-GetSlotType-response-checksum"></a>
Checksum of the `$LATEST` version of the slot type\.  
Type: String

 ** [createdDate](#API_GetSlotType_ResponseSyntax) **   <a name="lex-GetSlotType-response-createdDate"></a>
The date that the slot type was created\.  
Type: Timestamp

 ** [description](#API_GetSlotType_ResponseSyntax) **   <a name="lex-GetSlotType-response-description"></a>
A description of the slot type\.  
Type: String  
Length Constraints: Minimum length of 0\. Maximum length of 200\.

 ** [enumerationValues](#API_GetSlotType_ResponseSyntax) **   <a name="lex-GetSlotType-response-enumerationValues"></a>
A list of `EnumerationValue` objects that defines the values that the slot type can take\.  
Type: Array of [EnumerationValue](API_EnumerationValue.md) objects  
Array Members: Minimum number of 0 items\. Maximum number of 10000 items\.

 ** [lastUpdatedDate](#API_GetSlotType_ResponseSyntax) **   <a name="lex-GetSlotType-response-lastUpdatedDate"></a>
The date that the slot type was updated\. When you create a resource, the creation date and last update date are the same\.  
Type: Timestamp

 ** [name](#API_GetSlotType_ResponseSyntax) **   <a name="lex-GetSlotType-response-name"></a>
The name of the slot type\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `^([A-Za-z]_?)+$` 

 ** [parentSlotTypeSignature](#API_GetSlotType_ResponseSyntax) **   <a name="lex-GetSlotType-response-parentSlotTypeSignature"></a>
The built\-in slot type used as a parent for the slot type\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `^((AMAZON\.)_?|[A-Za-z]_?)+` 

 ** [slotTypeConfigurations](#API_GetSlotType_ResponseSyntax) **   <a name="lex-GetSlotType-response-slotTypeConfigurations"></a>
Configuration information that extends the parent built\-in slot type\.  
Type: Array of [SlotTypeConfiguration](API_SlotTypeConfiguration.md) objects  
Array Members: Minimum number of 0 items\. Maximum number of 10 items\.

 ** [valueSelectionStrategy](#API_GetSlotType_ResponseSyntax) **   <a name="lex-GetSlotType-response-valueSelectionStrategy"></a>
The strategy that Amazon Lex uses to determine the value of the slot\. For more information, see [PutSlotType](API_PutSlotType.md)\.  
Type: String  
Valid Values:` ORIGINAL_VALUE | TOP_RESOLUTION` 

 ** [version](#API_GetSlotType_ResponseSyntax) **   <a name="lex-GetSlotType-response-version"></a>
The version of the slot type\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 64\.  
Pattern: `\$LATEST|[0-9]+` 

## Errors<a name="API_GetSlotType_Errors"></a>

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

## See Also<a name="API_GetSlotType_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/lex-models-2017-04-19/GetSlotType) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/lex-models-2017-04-19/GetSlotType) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/lex-models-2017-04-19/GetSlotType) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/lex-models-2017-04-19/GetSlotType) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/lex-models-2017-04-19/GetSlotType) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/lex-models-2017-04-19/GetSlotType) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/lex-models-2017-04-19/GetSlotType) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/lex-models-2017-04-19/GetSlotType) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/lex-models-2017-04-19/GetSlotType) 