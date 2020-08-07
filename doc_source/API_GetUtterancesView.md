# GetUtterancesView<a name="API_GetUtterancesView"></a>

Use the `GetUtterancesView` operation to get information about the utterances that your users have made to your bot\. You can use this list to tune the utterances that your bot responds to\.

For example, say that you have created a bot to order flowers\. After your users have used your bot for a while, use the `GetUtterancesView` operation to see the requests that they have made and whether they have been successful\. You might find that the utterance "I want flowers" is not being recognized\. You could add this utterance to the `OrderFlowers` intent so that your bot recognizes that utterance\.

After you publish a new version of a bot, you can get information about the old version and the new so that you can compare the performance across the two versions\. 

Utterance statistics are generated once a day\. Data is available for the last 15 days\. You can request information for up to 5 versions of your bot in each request\. Amazon Lex returns the most frequent utterances received by the bot in the last 15 days\. The response contains information about a maximum of 100 utterances for each version\.

If you set `childDirected` field to true when you created your bot, or if you opted out of participating in improving Amazon Lex, utterances are not available\.

This operation requires permissions for the `lex:GetUtterancesView` action\.

## Request Syntax<a name="API_GetUtterancesView_RequestSyntax"></a>

```
GET /bots/botname/utterances?view=aggregation&bot_versions=botVersions&status_type=statusType HTTP/1.1
```

## URI Request Parameters<a name="API_GetUtterancesView_RequestParameters"></a>

The request uses the following URI parameters\.

 ** [botname](#API_GetUtterancesView_RequestSyntax) **   <a name="lex-GetUtterancesView-request-botName"></a>
The name of the bot for which utterance information should be returned\.  
Length Constraints: Minimum length of 2\. Maximum length of 50\.  
Pattern: `^([A-Za-z]_?)+$`   
Required: Yes

 ** [botVersions](#API_GetUtterancesView_RequestSyntax) **   <a name="lex-GetUtterancesView-request-botVersions"></a>
An array of bot versions for which utterance information should be returned\. The limit is 5 versions per request\.  
Array Members: Minimum number of 1 item\. Maximum number of 5 items\.  
Length Constraints: Minimum length of 1\. Maximum length of 64\.  
Pattern: `\$LATEST|[0-9]+`   
Required: Yes

 ** [statusType](#API_GetUtterancesView_RequestSyntax) **   <a name="lex-GetUtterancesView-request-statusType"></a>
To return utterances that were recognized and handled, use `Detected`\. To return utterances that were not recognized, use `Missed`\.  
Valid Values:` Detected | Missed`   
Required: Yes

## Request Body<a name="API_GetUtterancesView_RequestBody"></a>

The request does not have a request body\.

## Response Syntax<a name="API_GetUtterancesView_ResponseSyntax"></a>

```
HTTP/1.1 200
Content-type: application/json

{
   "botName": "string",
   "utterances": [ 
      { 
         "botVersion": "string",
         "utterances": [ 
            { 
               "count": number,
               "distinctUsers": number,
               "firstUtteredDate": number,
               "lastUtteredDate": number,
               "utteranceString": "string"
            }
         ]
      }
   ]
}
```

## Response Elements<a name="API_GetUtterancesView_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

 ** [botName](#API_GetUtterancesView_ResponseSyntax) **   <a name="lex-GetUtterancesView-response-botName"></a>
The name of the bot for which utterance information was returned\.  
Type: String  
Length Constraints: Minimum length of 2\. Maximum length of 50\.  
Pattern: `^([A-Za-z]_?)+$` 

 ** [utterances](#API_GetUtterancesView_ResponseSyntax) **   <a name="lex-GetUtterancesView-response-utterances"></a>
An array of [UtteranceList](API_UtteranceList.md) objects, each containing a list of [UtteranceData](API_UtteranceData.md) objects describing the utterances that were processed by your bot\. The response contains a maximum of 100 `UtteranceData` objects for each version\. Amazon Lex returns the most frequent utterances received by the bot in the last 15 days\.  
Type: Array of [UtteranceList](API_UtteranceList.md) objects

## Errors<a name="API_GetUtterancesView_Errors"></a>

 **BadRequestException**   
The request is not well formed\. For example, a value is invalid or a required field is missing\. Check the field values, and try again\.  
HTTP Status Code: 400

 **InternalFailureException**   
An internal Amazon Lex error occurred\. Try your request again\.  
HTTP Status Code: 500

 **LimitExceededException**   
The request exceeded a limit\. Try your request again\.  
HTTP Status Code: 429

## See Also<a name="API_GetUtterancesView_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS Command Line Interface](https://docs.aws.amazon.com/goto/aws-cli/lex-models-2017-04-19/GetUtterancesView) 
+  [AWS SDK for \.NET](https://docs.aws.amazon.com/goto/DotNetSDKV3/lex-models-2017-04-19/GetUtterancesView) 
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/lex-models-2017-04-19/GetUtterancesView) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/lex-models-2017-04-19/GetUtterancesView) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/lex-models-2017-04-19/GetUtterancesView) 
+  [AWS SDK for JavaScript](https://docs.aws.amazon.com/goto/AWSJavaScriptSDK/lex-models-2017-04-19/GetUtterancesView) 
+  [AWS SDK for PHP V3](https://docs.aws.amazon.com/goto/SdkForPHPV3/lex-models-2017-04-19/GetUtterancesView) 
+  [AWS SDK for Python](https://docs.aws.amazon.com/goto/boto3/lex-models-2017-04-19/GetUtterancesView) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/lex-models-2017-04-19/GetUtterancesView) 