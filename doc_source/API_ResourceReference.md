# ResourceReference<a name="API_ResourceReference"></a>

Describes the resource that refers to the resource that you are attempting to delete\. This object is returned as part of the `ResourceInUseException` exception\. 

## Contents<a name="API_ResourceReference_Contents"></a>

 **name**   <a name="lex-Type-ResourceReference-name"></a>
The name of the resource that is using the resource that you are trying to delete\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `[a-zA-Z_]+`   
Required: No

 **version**   <a name="lex-Type-ResourceReference-version"></a>
The version of the resource that is using the resource that you are trying to delete\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 64\.  
Pattern: `\$LATEST|[0-9]+`   
Required: No

## See Also<a name="API_ResourceReference_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/lex-models-2017-04-19/ResourceReference) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/lex-models-2017-04-19/ResourceReference) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/lex-models-2017-04-19/ResourceReference) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/lex-models-2017-04-19/ResourceReference) 