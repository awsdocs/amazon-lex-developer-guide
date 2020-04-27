# Statement<a name="API_Statement"></a>

A collection of messages that convey information to the user\. At runtime, Amazon Lex selects the message to convey\. 

## Contents<a name="API_Statement_Contents"></a>

 **messages**   <a name="lex-Type-Statement-messages"></a>
A collection of message objects\.  
Type: Array of [Message](API_Message.md) objects  
Array Members: Minimum number of 1 item\. Maximum number of 15 items\.  
Required: Yes

 **responseCard**   <a name="lex-Type-Statement-responseCard"></a>
 At runtime, if the client is using the [PostText](http://docs.aws.amazon.com/lex/latest/dg/API_runtime_PostText.html) API, Amazon Lex includes the response card in the response\. It substitutes all of the session attributes and slot values for placeholders in the response card\.   
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 50000\.  
Required: No

## See Also<a name="API_Statement_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/lex-models-2017-04-19/Statement) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/lex-models-2017-04-19/Statement) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/lex-models-2017-04-19/Statement) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/lex-models-2017-04-19/Statement) 