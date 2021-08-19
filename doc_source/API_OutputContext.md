# OutputContext<a name="API_OutputContext"></a>

The specification of an output context that is set when an intent is fulfilled\.

## Contents<a name="API_OutputContext_Contents"></a>

 **name**   <a name="lex-Type-OutputContext-name"></a>
The name of the context\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `^([A-Za-z]_?)+$`   
Required: Yes

 **timeToLiveInSeconds**   <a name="lex-Type-OutputContext-timeToLiveInSeconds"></a>
The number of seconds that the context should be active after it is first sent in a `PostContent` or `PostText` response\. You can set the value between 5 and 86,400 seconds \(24 hours\)\.  
Type: Integer  
Valid Range: Minimum value of 5\. Maximum value of 86400\.  
Required: Yes

 **turnsToLive**   <a name="lex-Type-OutputContext-turnsToLive"></a>
The number of conversation turns that the context should be active\. A conversation turn is one `PostContent` or `PostText` request and the corresponding response from Amazon Lex\.  
Type: Integer  
Valid Range: Minimum value of 1\. Maximum value of 20\.  
Required: Yes

## See Also<a name="API_OutputContext_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/lex-models-2017-04-19/OutputContext) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/lex-models-2017-04-19/OutputContext) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/lex-models-2017-04-19/OutputContext) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/lex-models-2017-04-19/OutputContext) 