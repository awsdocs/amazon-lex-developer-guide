# ActiveContextTimeToLive<a name="API_runtime_ActiveContextTimeToLive"></a>

The length of time or number of turns that a context remains active\.

## Contents<a name="API_runtime_ActiveContextTimeToLive_Contents"></a>

 **timeToLiveInSeconds**   <a name="lex-Type-runtime_ActiveContextTimeToLive-timeToLiveInSeconds"></a>
The number of seconds that the context should be active after it is first sent in a `PostContent` or `PostText` response\. You can set the value between 5 and 86,400 seconds \(24 hours\)\.  
Type: Integer  
Valid Range: Minimum value of 5\. Maximum value of 86400\.  
Required: No

 **turnsToLive**   <a name="lex-Type-runtime_ActiveContextTimeToLive-turnsToLive"></a>
The number of conversation turns that the context should be active\. A conversation turn is one `PostContent` or `PostText` request and the corresponding response from Amazon Lex\.  
Type: Integer  
Valid Range: Minimum value of 1\. Maximum value of 20\.  
Required: No

## See Also<a name="API_runtime_ActiveContextTimeToLive_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/runtime.lex-2016-11-28/ActiveContextTimeToLive) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/runtime.lex-2016-11-28/ActiveContextTimeToLive) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/runtime.lex-2016-11-28/ActiveContextTimeToLive) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/runtime.lex-2016-11-28/ActiveContextTimeToLive) 