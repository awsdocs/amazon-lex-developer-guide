# Intent<a name="API_Intent"></a>

Identifies the specific version of an intent\.

## Contents<a name="API_Intent_Contents"></a>

 **intentName**   <a name="lex-Type-Intent-intentName"></a>
The name of the intent\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `^([A-Za-z]_?)+$`   
Required: Yes

 **intentVersion**   <a name="lex-Type-Intent-intentVersion"></a>
The version of the intent\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 64\.  
Pattern: `\$LATEST|[0-9]+`   
Required: Yes

## See Also<a name="API_Intent_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/lex-models-2017-04-19/Intent) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/lex-models-2017-04-19/Intent) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/lex-models-2017-04-19/Intent) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/lex-models-2017-04-19/Intent) 