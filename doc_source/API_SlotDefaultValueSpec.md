# SlotDefaultValueSpec<a name="API_SlotDefaultValueSpec"></a>

Contains the default values for a slot\. Default values are used when Amazon Lex hasn't determined a value for a slot\.

## Contents<a name="API_SlotDefaultValueSpec_Contents"></a>

 **defaultValueList**   <a name="lex-Type-SlotDefaultValueSpec-defaultValueList"></a>
The default values for a slot\. You can specify more than one default\. For example, you can specify a default value to use from a matching context variable, a session attribute, or a fixed value\.  
The default value chosen is selected based on the order that you specify them in the list\. For example, if you specify a context variable and a fixed value in that order, Amazon Lex uses the context variable if it is available, else it uses the fixed value\.  
Type: Array of [SlotDefaultValue](API_SlotDefaultValue.md) objects  
Array Members: Minimum number of 0 items\. Maximum number of 10 items\.  
Required: Yes

## See Also<a name="API_SlotDefaultValueSpec_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/lex-models-2017-04-19/SlotDefaultValueSpec) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/lex-models-2017-04-19/SlotDefaultValueSpec) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/lex-models-2017-04-19/SlotDefaultValueSpec) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/lex-models-2017-04-19/SlotDefaultValueSpec) 