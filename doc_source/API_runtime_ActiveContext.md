# ActiveContext<a name="API_runtime_ActiveContext"></a>

A context is a variable that contains information about the current state of the conversation between a user and Amazon Lex\. Context can be set automatically by Amazon Lex when an intent is fulfilled, or it can be set at runtime using the `PutContent`, `PutText`, or `PutSession` operation\.

## Contents<a name="API_runtime_ActiveContext_Contents"></a>

 **name**   <a name="lex-Type-runtime_ActiveContext-name"></a>
The name of the context\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `^([A-Za-z]_?)+$`   
Required: Yes

 **parameters**   <a name="lex-Type-runtime_ActiveContext-parameters"></a>
State variables for the current context\. You can use these values as default values for slots in subsequent events\.  
Type: String to string map  
Map Entries: Minimum number of 0 items\. Maximum number of 10 items\.  
Key Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Value Length Constraints: Minimum length of 1\. Maximum length of 1024\.  
Required: Yes

 **timeToLive**   <a name="lex-Type-runtime_ActiveContext-timeToLive"></a>
The length of time or number of turns that a context remains active\.  
Type: [ActiveContextTimeToLive](API_runtime_ActiveContextTimeToLive.md) object  
Required: Yes

## See Also<a name="API_runtime_ActiveContext_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/runtime.lex-2016-11-28/ActiveContext) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/runtime.lex-2016-11-28/ActiveContext) 
+  [AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/runtime.lex-2016-11-28/ActiveContext) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/runtime.lex-2016-11-28/ActiveContext) 