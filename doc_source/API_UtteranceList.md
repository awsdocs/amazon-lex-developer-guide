# UtteranceList<a name="API_UtteranceList"></a>

Provides a list of utterances that have been made to a specific version of your bot\. The list contains a maximum of 100 utterances\.

## Contents<a name="API_UtteranceList_Contents"></a>

 **botVersion**   <a name="lex-Type-UtteranceList-botVersion"></a>
The version of the bot that processed the list\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 64\.  
Pattern: `\$LATEST|[0-9]+`   
Required: No

 **utterances**   <a name="lex-Type-UtteranceList-utterances"></a>
One or more [UtteranceData](API_UtteranceData.md) objects that contain information about the utterances that have been made to a bot\. The maximum number of object is 100\.  
Type: Array of [UtteranceData](API_UtteranceData.md) objects  
Required: No

## See Also<a name="API_UtteranceList_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/lex-models-2017-04-19/UtteranceList) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/lex-models-2017-04-19/UtteranceList) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/lex-models-2017-04-19/UtteranceList) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/lex-models-2017-04-19/UtteranceList) 