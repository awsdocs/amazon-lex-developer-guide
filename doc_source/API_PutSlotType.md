# PutSlotType<a name="API_PutSlotType"></a>

Creates a custom slot type or replaces an existing custom slot type\.

To create a custom slot type, specify a name for the slot type and a set of enumeration values, which are the values that a slot of this type can assume\. For more information, see [Amazon Lex: How It Works](how-it-works.md)\.

If you specify the name of an existing slot type, the fields in the request replace the existing values in the `$LATEST` version of the slot type\. Amazon Lex removes the fields that you don't provide in the request\. If you don't specify required fields, Amazon Lex throws an exception\. When you update the `$LATEST` version of a slot type, if a bot uses the `$LATEST` version of an intent that contains the slot type, the bot's `status` field is set to `NOT_BUILT`\.

This operation requires permissions for the `lex:PutSlotType` action\.

## Request Syntax<a name="API_PutSlotType_RequestSyntax"></a>

```
PUT /slottypes/name/versions/$LATEST HTTP/1.1
Content-type: application/json

{
   "checksum": "string",
   "description": "string",
   "enumerationValues": [ 
      { 
         "synonyms": [ "string" ],
         "value": "string"
      }
   ],
   "valueSelectionStrategy": "string"
}
```

## URI Request Parameters<a name="API_PutSlotType_RequestParameters"></a>

The request requires the following URI parameters\.

 ** name **   
The name of the slot type\. The name is *not* case sensitive\.   
The name can't match a built\-in slot type name, or a built\-in slot type name with "AMAZON\." removed\. For example, because there is a built\-in slot type called `AMAZON.DATE`, you can't create a custom slot type called `DATE`\.  
For a list of built\-in slot types, see [Slot Type Reference](https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit/docs/built-in-intent-ref/slot-type-reference) in the *Alexa Skills Kit*\.  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `^([A-Za-z]_?)+$` 

## Request Body<a name="API_PutSlotType_RequestBody"></a>

The request accepts the following data in JSON format\.

 ** checksum **   
Identifies a specific revision of the `$LATEST` version\.  
When you create a new slot type, leave the `checksum` field blank\. If you specify a checksum you get a `BadRequestException` exception\.  
When you want to update a slot type, set the `checksum` field to the checksum of the most recent revision of the `$LATEST` version\. If you don't specify the ` checksum` field, or if the checksum does not match the `$LATEST` version, you get a `PreconditionFailedException` exception\.  
Type: String  
Required: No

 ** description **   
A description of the slot type\.  
Type: String  
Length Constraints: Minimum length of 0\. Maximum length of 200\.  
Required: No

 ** enumerationValues **   
A list of `EnumerationValue` objects that defines the values that the slot type can take\. Each value can have a list of `synonyms`, which are additional values that help train the machine learning model about the values that it resolves for a slot\.   
When Amazon Lex resolves a slot value, it generates a resolution list that contains up to five possible values for the slot\. If you are using a Lambda function, this resolution list is passed to the function\. If you are not using a Lambda function you can choose to return the value that the user entered or the first value in the resolution list as the slot value\. The `valueSelectionStrategy` field indicates the option to use\.   
Type: Array of [EnumerationValue](API_EnumerationValue.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 10000 items\.  
Required: No

 ** valueSelectionStrategy **   
Determines the slot resolution strategy that Amazon Lex uses to return slot type values\. The field can be set to one of the following values:  

+  `ORIGINAL_VALUE` \- Returns the value entered by the user, if the user value is similar to the slot value\.

+  `TOP_RESOLUTION` \- If there is a resolution list for the slot, return the first value in the resolution list as the slot type value\. If there is no resolution list, null is returned\.
If you don't specify the `valueSelectionStrategy`, the default is `ORIGINAL_VALUE`\.  
Type: String  
Valid Values:` ORIGINAL_VALUE | TOP_RESOLUTION`   
Required: No

## Response Syntax<a name="API_PutSlotType_ResponseSyntax"></a>

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
   "valueSelectionStrategy": "string",
   "version": "string"
}
```

## Response Elements<a name="API_PutSlotType_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** checksum **   
Checksum of the `$LATEST` version of the slot type\.  
Type: String

 ** createdDate **   
The date that the slot type was created\.  
Type: Timestamp

 ** description **   
A description of the slot type\.  
Type: String  
Length Constraints: Minimum length of 0\. Maximum length of 200\.

 ** enumerationValues **   
A list of `EnumerationValue` objects that defines the values that the slot type can take\.  
Type: Array of [EnumerationValue](API_EnumerationValue.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 10000 items\.

 ** lastUpdatedDate **   
The date that the slot type was updated\. When you create a slot type, the creation date and last update date are the same\.  
Type: Timestamp

 ** name **   
The name of the slot type\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `^([A-Za-z]_?)+$` 

 ** valueSelectionStrategy **   
The slot resolution strategy that Amazon Lex uses to determine the value of the slot\. For more information, see [PutSlotType](#API_PutSlotType)\.  
Type: String  
Valid Values:` ORIGINAL_VALUE | TOP_RESOLUTION` 

 ** version **   
The version of the slot type\. For a new slot type, the version is always `$LATEST`\.   
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 64\.  
Pattern: `\$LATEST|[0-9]+` 

## Errors<a name="API_PutSlotType_Errors"></a>

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

 **PreconditionFailedException**   
 The checksum of the resource that you are trying to change does not match the checksum in the request\. Check the resource's checksum and try again\.  
HTTP Status Code: 412

## See Also<a name="API_PutSlotType_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:

+  [AWS Command Line Interface](http://docs.aws.amazon.com/goto/aws-cli/lex-models-2017-04-19/PutSlotType) 

+  [AWS SDK for \.NET](http://docs.aws.amazon.com/goto/DotNetSDKV3/lex-models-2017-04-19/PutSlotType) 

+  [AWS SDK for C\+\+](http://docs.aws.amazon.com/goto/SdkForCpp/lex-models-2017-04-19/PutSlotType) 

+  [AWS SDK for Go](http://docs.aws.amazon.com/goto/SdkForGoV1/lex-models-2017-04-19/PutSlotType) 

+  [AWS SDK for Java](http://docs.aws.amazon.com/goto/SdkForJava/lex-models-2017-04-19/PutSlotType) 

+  [AWS SDK for JavaScript](http://docs.aws.amazon.com/goto/AWSJavaScriptSDK/lex-models-2017-04-19/PutSlotType) 

+  [AWS SDK for PHP V3](http://docs.aws.amazon.com/goto/SdkForPHPV3/lex-models-2017-04-19/PutSlotType) 

+  [AWS SDK for Python](http://docs.aws.amazon.com/goto/boto3/lex-models-2017-04-19/PutSlotType) 

+  [AWS SDK for Ruby V2](http://docs.aws.amazon.com/goto/SdkForRubyV2/lex-models-2017-04-19/PutSlotType) 