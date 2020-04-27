# EnumerationValue<a name="API_EnumerationValue"></a>

Each slot type can have a set of values\. Each enumeration value represents a value the slot type can take\. 

For example, a pizza ordering bot could have a slot type that specifies the type of crust that the pizza should have\. The slot type could include the values 
+ thick
+ thin
+ stuffed

## Contents<a name="API_EnumerationValue_Contents"></a>

 **synonyms**   <a name="lex-Type-EnumerationValue-synonyms"></a>
Additional values related to the slot type value\.  
Type: Array of strings  
Length Constraints: Minimum length of 1\. Maximum length of 140\.  
Required: No

 **value**   <a name="lex-Type-EnumerationValue-value"></a>
The value of the slot type\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 140\.  
Required: Yes

## See Also<a name="API_EnumerationValue_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/lex-models-2017-04-19/EnumerationValue) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/lex-models-2017-04-19/EnumerationValue) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/lex-models-2017-04-19/EnumerationValue) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/lex-models-2017-04-19/EnumerationValue) 