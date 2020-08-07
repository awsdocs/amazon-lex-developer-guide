# Slot<a name="API_Slot"></a>

Identifies the version of a specific slot\.

## Contents<a name="API_Slot_Contents"></a>

 **description**   <a name="lex-Type-Slot-description"></a>
A description of the slot\.  
Type: String  
Length Constraints: Minimum length of 0\. Maximum length of 200\.  
Required: No

 **name**   <a name="lex-Type-Slot-name"></a>
The name of the slot\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `^([A-Za-z](-|_|.)?)+$`   
Required: Yes

 **obfuscationSetting**   <a name="lex-Type-Slot-obfuscationSetting"></a>
Determines whether a slot is obfuscated in conversation logs and stored utterances\. When you obfuscate a slot, the value is replaced by the slot name in curly braces \(\{\}\)\. For example, if the slot name is "full\_name", obfuscated values are replaced with "\{full\_name\}"\. For more information, see [ Slot Obfuscation ](https://docs.aws.amazon.com/lex/latest/dg/how-obfuscate.html)\.   
Type: String  
Valid Values:` NONE | DEFAULT_OBFUSCATION`   
Required: No

 **priority**   <a name="lex-Type-Slot-priority"></a>
 Directs Amazon Lex the order in which to elicit this slot value from the user\. For example, if the intent has two slots with priorities 1 and 2, AWS Amazon Lex first elicits a value for the slot with priority 1\.  
If multiple slots share the same priority, the order in which Amazon Lex elicits values is arbitrary\.  
Type: Integer  
Valid Range: Minimum value of 0\. Maximum value of 100\.  
Required: No

 **responseCard**   <a name="lex-Type-Slot-responseCard"></a>
 A set of possible responses for the slot type used by text\-based clients\. A user chooses an option from the response card, instead of using text to reply\.   
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 50000\.  
Required: No

 **sampleUtterances**   <a name="lex-Type-Slot-sampleUtterances"></a>
 If you know a specific pattern with which users might respond to an Amazon Lex request for a slot value, you can provide those utterances to improve accuracy\. This is optional\. In most cases, Amazon Lex is capable of understanding user utterances\.   
Type: Array of strings  
Array Members: Minimum number of 0 items\. Maximum number of 10 items\.  
Length Constraints: Minimum length of 1\. Maximum length of 200\.  
Required: No

 **slotConstraint**   <a name="lex-Type-Slot-slotConstraint"></a>
Specifies whether the slot is required or optional\.   
Type: String  
Valid Values:` Required | Optional`   
Required: Yes

 **slotType**   <a name="lex-Type-Slot-slotType"></a>
The type of the slot, either a custom slot type that you defined or one of the built\-in slot types\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 100\.  
Pattern: `^((AMAZON\.)_?|[A-Za-z]_?)+`   
Required: No

 **slotTypeVersion**   <a name="lex-Type-Slot-slotTypeVersion"></a>
The version of the slot type\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 64\.  
Pattern: `\$LATEST|[0-9]+`   
Required: No

 **valueElicitationPrompt**   <a name="lex-Type-Slot-valueElicitationPrompt"></a>
The prompt that Amazon Lex uses to elicit the slot value from the user\.  
Type: [Prompt](API_Prompt.md) object  
Required: No

## See Also<a name="API_Slot_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/lex-models-2017-04-19/Slot) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/lex-models-2017-04-19/Slot) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/lex-models-2017-04-19/Slot) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/lex-models-2017-04-19/Slot) 