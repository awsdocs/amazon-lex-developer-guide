# ResponseCard<a name="API_runtime_ResponseCard"></a>

If you configure a response card when creating your bots, Amazon Lex substitutes the session attributes and slot values that are available, and then returns it\. The response card can also come from a Lambda function \( `dialogCodeHook` and `fulfillmentActivity` on an intent\)\.

## Contents<a name="API_runtime_ResponseCard_Contents"></a>

 **contentType**   
The content type of the response\.  
Type: String  
Valid Values:` application/vnd.amazonaws.card.generic`   
Required: No

 **genericAttachments**   
An array of attachment objects representing options\.  
Type: Array of [GenericAttachment](API_runtime_GenericAttachment.md) objects  
Array Members: Minimum number of 0 items\. Maximum number of 10 items\.  
Required: No

 **version**   
The version of the response card format\.  
Type: String  
Required: No

## See Also<a name="API_runtime_ResponseCard_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:

+  [AWS SDK for C\+\+](http://docs.aws.amazon.com/goto/SdkForCpp/runtime.lex-2016-11-28/ResponseCard) 

+  [AWS SDK for Go](http://docs.aws.amazon.com/goto/SdkForGoV1/runtime.lex-2016-11-28/ResponseCard) 

+  [AWS SDK for Java](http://docs.aws.amazon.com/goto/SdkForJava/runtime.lex-2016-11-28/ResponseCard) 

+  [AWS SDK for Ruby V2](http://docs.aws.amazon.com/goto/SdkForRubyV2/runtime.lex-2016-11-28/ResponseCard) 