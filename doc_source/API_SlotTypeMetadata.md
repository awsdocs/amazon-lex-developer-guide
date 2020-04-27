# SlotTypeMetadata<a name="API_SlotTypeMetadata"></a>

Provides information about a slot type\.\.

## Contents<a name="API_SlotTypeMetadata_Contents"></a>

 **createdDate**   <a name="lex-Type-SlotTypeMetadata-createdDate"></a>
The date that the slot type was created\.  
Type: Timestamp  
Required: No

 **description**   <a name="lex-Type-SlotTypeMetadata-description"></a>
A description of the slot type\.  
Type: String  
Length Constraints: Minimum length of 0\. Maximum length of 200\.  
Required: No

 **lastUpdatedDate**   <a name="lex-Type-SlotTypeMetadata-lastUpdatedDate"></a>
The date that the slot type was updated\. When you create a resource, the creation date and last updated date are the same\.   
Type: Timestamp  
Required: No

 **name**   <a name="lex-Type-SlotTypeMetadata-name"></a>
The name of the slot type\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `^([A-Za-z]_?)+$`   
Required: No

 **version**   <a name="lex-Type-SlotTypeMetadata-version"></a>
The version of the slot type\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 64\.  
Pattern: `\$LATEST|[0-9]+`   
Required: No

## See Also<a name="API_SlotTypeMetadata_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/lex-models-2017-04-19/SlotTypeMetadata) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/lex-models-2017-04-19/SlotTypeMetadata) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/lex-models-2017-04-19/SlotTypeMetadata) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/lex-models-2017-04-19/SlotTypeMetadata) 