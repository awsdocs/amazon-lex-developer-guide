# Tag<a name="API_Tag"></a>

A list of key/value pairs that identify a bot, bot alias, or bot channel\. Tag keys and values can consist of Unicode letters, digits, white space, and any of the following symbols: \_ \. : / = \+ \- @\. 

## Contents<a name="API_Tag_Contents"></a>

 **key**   <a name="lex-Type-Tag-key"></a>
The key for the tag\. Keys are not case\-sensitive and must be unique\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 128\.  
Required: Yes

 **value**   <a name="lex-Type-Tag-value"></a>
The value associated with a key\. The value may be an empty string but it can't be null\.  
Type: String  
Length Constraints: Minimum length of 0\. Maximum length of 256\.  
Required: Yes

## See Also<a name="API_Tag_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/lex-models-2017-04-19/Tag) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/lex-models-2017-04-19/Tag) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/lex-models-2017-04-19/Tag) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/lex-models-2017-04-19/Tag) 