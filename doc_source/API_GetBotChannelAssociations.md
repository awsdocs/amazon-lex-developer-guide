# GetBotChannelAssociations<a name="API_GetBotChannelAssociations"></a>

 Returns a list of all of the channels associated with the specified bot\. 

The `GetBotChannelAssociations` operation requires permissions for the `lex:GetBotChannelAssociations` action\.

## Request Syntax<a name="API_GetBotChannelAssociations_RequestSyntax"></a>

```
GET /bots/botName/aliases/aliasName/channels/?maxResults=maxResults&nameContains=nameContains&nextToken=nextToken HTTP/1.1
```

## URI Request Parameters<a name="API_GetBotChannelAssociations_RequestParameters"></a>

The request requires the following URI parameters\.

 ** botAlias **   
An alias pointing to the specific version of the Amazon Lex bot to which this association is being made\.  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `^(-|^([A-Za-z]_?)+$)$` 

 ** botName **   
The name of the Amazon Lex bot in the association\.  
Length Constraints: Minimum length of 2\. Maximum length of 50\.  
Pattern: `^([A-Za-z]_?)+$` 

 ** maxResults **   
The maximum number of associations to return in the response\. The default is 50\.   
Valid Range: Minimum value of 1\. Maximum value of 50\.

 ** nameContains **   
Substring to match in channel association names\. An association will be returned if any part of its name matches the substring\. For example, "xyz" matches both "xyzabc" and "abcxyz\." To return all bot channel associations, use a hyphen \("\-"\) as the `nameContains` parameter\.  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `^([A-Za-z]_?)+$` 

 ** nextToken **   
A pagination token for fetching the next page of associations\. If the response to this call is truncated, Amazon Lex returns a pagination token in the response\. To fetch the next page of associations, specify the pagination token in the next request\. 

## Request Body<a name="API_GetBotChannelAssociations_RequestBody"></a>

The request does not have a request body\.

## Response Syntax<a name="API_GetBotChannelAssociations_ResponseSyntax"></a>

```
HTTP/1.1 200
Content-type: application/json

{
   "botChannelAssociations": [ 
      { 
         "botAlias": "string",
         "botConfiguration": { 
            "string" : "string" 
         },
         "botName": "string",
         "createdDate": number,
         "description": "string",
         "failureReason": "string",
         "name": "string",
         "status": "string",
         "type": "string"
      }
   ],
   "nextToken": "string"
}
```

## Response Elements<a name="API_GetBotChannelAssociations_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** botChannelAssociations **   
An array of objects, one for each association, that provides information about the Amazon Lex bot and its association with the channel\.   
Type: Array of [BotChannelAssociation](API_BotChannelAssociation.md) objects

 ** nextToken **   
A pagination token that fetches the next page of associations\. If the response to this call is truncated, Amazon Lex returns a pagination token in the response\. To fetch the next page of associations, specify the pagination token in the next request\.   
Type: String

## Errors<a name="API_GetBotChannelAssociations_Errors"></a>

 **BadRequestException**   
The request is not well formed\. For example, a value is invalid or a required field is missing\. Check the field values, and try again\.  
HTTP Status Code: 400

 **InternalFailureException**   
An internal Amazon Lex error occurred\. Try your request again\.  
HTTP Status Code: 500

 **LimitExceededException**   
The request exceeded a limit\. Try your request again\.  
HTTP Status Code: 429

## See Also<a name="API_GetBotChannelAssociations_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:

+  [AWS Command Line Interface](http://docs.aws.amazon.com/goto/aws-cli/lex-models-2017-04-19/GetBotChannelAssociations) 

+  [AWS SDK for \.NET](http://docs.aws.amazon.com/goto/DotNetSDKV3/lex-models-2017-04-19/GetBotChannelAssociations) 

+  [AWS SDK for C\+\+](http://docs.aws.amazon.com/goto/SdkForCpp/lex-models-2017-04-19/GetBotChannelAssociations) 

+  [AWS SDK for Go](http://docs.aws.amazon.com/goto/SdkForGoV1/lex-models-2017-04-19/GetBotChannelAssociations) 

+  [AWS SDK for Java](http://docs.aws.amazon.com/goto/SdkForJava/lex-models-2017-04-19/GetBotChannelAssociations) 

+  [AWS SDK for JavaScript](http://docs.aws.amazon.com/goto/AWSJavaScriptSDK/lex-models-2017-04-19/GetBotChannelAssociations) 

+  [AWS SDK for PHP V3](http://docs.aws.amazon.com/goto/SdkForPHPV3/lex-models-2017-04-19/GetBotChannelAssociations) 

+  [AWS SDK for Python](http://docs.aws.amazon.com/goto/boto3/lex-models-2017-04-19/GetBotChannelAssociations) 

+  [AWS SDK for Ruby V2](http://docs.aws.amazon.com/goto/SdkForRubyV2/lex-models-2017-04-19/GetBotChannelAssociations) 