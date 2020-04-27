# Prompt<a name="API_Prompt"></a>

Obtains information from the user\. To define a prompt, provide one or more messages and specify the number of attempts to get information from the user\. If you provide more than one message, Amazon Lex chooses one of the messages to use to prompt the user\. For more information, see [Amazon Lex: How It Works](how-it-works.md)\.

## Contents<a name="API_Prompt_Contents"></a>

 **maxAttempts**   <a name="lex-Type-Prompt-maxAttempts"></a>
The number of times to prompt the user for information\.  
Type: Integer  
Valid Range: Minimum value of 1\. Maximum value of 5\.  
Required: Yes

 **messages**   <a name="lex-Type-Prompt-messages"></a>
An array of objects, each of which provides a message string and its type\. You can specify the message string in plain text or in Speech Synthesis Markup Language \(SSML\)\.  
Type: Array of [Message](API_Message.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 15 items\.  
Required: Yes

 **responseCard**   <a name="lex-Type-Prompt-responseCard"></a>
A response card\. Amazon Lex uses this prompt at runtime, in the `PostText` API response\. It substitutes session attributes and slot values for placeholders in the response card\. For more information, see [Example: Using a Response Card](ex-resp-card.md)\.   
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 50000\.  
Required: No

## See Also<a name="API_Prompt_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/lex-models-2017-04-19/Prompt) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/lex-models-2017-04-19/Prompt) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/lex-models-2017-04-19/Prompt) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/lex-models-2017-04-19/Prompt) 