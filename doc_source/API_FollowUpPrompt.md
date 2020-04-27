# FollowUpPrompt<a name="API_FollowUpPrompt"></a>

A prompt for additional activity after an intent is fulfilled\. For example, after the `OrderPizza` intent is fulfilled, you might prompt the user to find out whether the user wants to order drinks\.

## Contents<a name="API_FollowUpPrompt_Contents"></a>

 **prompt**   <a name="lex-Type-FollowUpPrompt-prompt"></a>
Prompts for information from the user\.   
Type: [Prompt](API_Prompt.md) object  
Required: Yes

 **rejectionStatement**   <a name="lex-Type-FollowUpPrompt-rejectionStatement"></a>
If the user answers "no" to the question defined in the `prompt` field, Amazon Lex responds with this statement to acknowledge that the intent was canceled\.   
Type: [Statement](API_Statement.md) object  
Required: Yes

## See Also<a name="API_FollowUpPrompt_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/lex-models-2017-04-19/FollowUpPrompt) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/lex-models-2017-04-19/FollowUpPrompt) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/lex-models-2017-04-19/FollowUpPrompt) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/lex-models-2017-04-19/FollowUpPrompt) 