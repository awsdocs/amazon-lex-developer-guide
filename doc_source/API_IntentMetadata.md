# IntentMetadata<a name="API_IntentMetadata"></a>

Provides information about an intent\.

## Contents<a name="API_IntentMetadata_Contents"></a>

 **createdDate**   <a name="lex-Type-IntentMetadata-createdDate"></a>
The date that the intent was created\.  
Type: Timestamp  
Required: No

 **description**   <a name="lex-Type-IntentMetadata-description"></a>
A description of the intent\.  
Type: String  
Length Constraints: Minimum length of 0\. Maximum length of 200\.  
Required: No

 **lastUpdatedDate**   <a name="lex-Type-IntentMetadata-lastUpdatedDate"></a>
The date that the intent was updated\. When you create an intent, the creation date and last updated date are the same\.  
Type: Timestamp  
Required: No

 **name**   <a name="lex-Type-IntentMetadata-name"></a>
The name of the intent\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `^([A-Za-z]_?)+$`   
Required: No

 **version**   <a name="lex-Type-IntentMetadata-version"></a>
The version of the intent\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 64\.  
Pattern: `\$LATEST|[0-9]+`   
Required: No

## See Also<a name="API_IntentMetadata_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/lex-models-2017-04-19/IntentMetadata) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/lex-models-2017-04-19/IntentMetadata) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/lex-models-2017-04-19/IntentMetadata) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/lex-models-2017-04-19/IntentMetadata) 