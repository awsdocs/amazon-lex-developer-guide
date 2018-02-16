# ResourceReference<a name="API_ResourceReference"></a>

Describes the resource that refers to the resource that you are attempting to delete\. This object is returned as part of the `ResourceInUseException` exception\. 

## Contents<a name="API_ResourceReference_Contents"></a>

 **name**   
The name of the resource that is using the resource that you are trying to delete\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `[a-zA-Z_]+`   
Required: No

 **version**   
The version of the resource that is using the resource that you are trying to delete\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 64\.  
Pattern: `\$LATEST|[0-9]+`   
Required: No

## See Also<a name="API_ResourceReference_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:

+  [AWS SDK for C\+\+](http://docs.aws.amazon.com/goto/SdkForCpp/lex-models-2017-04-19/ResourceReference) 

+  [AWS SDK for Go](http://docs.aws.amazon.com/goto/SdkForGoV1/lex-models-2017-04-19/ResourceReference) 

+  [AWS SDK for Java](http://docs.aws.amazon.com/goto/SdkForJava/lex-models-2017-04-19/ResourceReference) 

+  [AWS SDK for Ruby V2](http://docs.aws.amazon.com/goto/SdkForRubyV2/lex-models-2017-04-19/ResourceReference) 