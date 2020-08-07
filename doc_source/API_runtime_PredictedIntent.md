# PredictedIntent<a name="API_runtime_PredictedIntent"></a>

An intent that Amazon Lex suggests satisfies the user's intent\. Includes the name of the intent, the confidence that Amazon Lex has that the user's intent is satisfied, and the slots defined for the intent\.

## Contents<a name="API_runtime_PredictedIntent_Contents"></a>

 **intentName**   <a name="lex-Type-runtime_PredictedIntent-intentName"></a>
The name of the intent that Amazon Lex suggests satisfies the user's intent\.  
Type: String  
Required: No

 **nluIntentConfidence**   <a name="lex-Type-runtime_PredictedIntent-nluIntentConfidence"></a>
Indicates how confident Amazon Lex is that an intent satisfies the user's intent\.  
Type: [IntentConfidence](API_runtime_IntentConfidence.md) object  
Required: No

 **slots**   <a name="lex-Type-runtime_PredictedIntent-slots"></a>
The slot and slot values associated with the predicted intent\.  
Type: String to string map  
Required: No

## See Also<a name="API_runtime_PredictedIntent_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/runtime.lex-2016-11-28/PredictedIntent) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/runtime.lex-2016-11-28/PredictedIntent) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/runtime.lex-2016-11-28/PredictedIntent) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/runtime.lex-2016-11-28/PredictedIntent) 