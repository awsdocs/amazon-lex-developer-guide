# GenericAttachment<a name="API_runtime_GenericAttachment"></a>

Represents an option rendered to the user when a prompt is shown\. It could be an image, a button, a link, or text\. 

## Contents<a name="API_runtime_GenericAttachment_Contents"></a>

 **attachmentLinkUrl**   
The URL of an attachment to the response card\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Required: No

 **buttons**   
The list of options to show to the user\.  
Type: Array of [Button](API_runtime_Button.md) objects  
Array Members: Minimum number of 0 items\. Maximum number of 5 items\.  
Required: No

 **imageUrl**   
The URL of an image that is displayed to the user\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Required: No

 **subTitle**   
The subtitle shown below the title\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 80\.  
Required: No

 **title**   
The title of the option\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 80\.  
Required: No

## See Also<a name="API_runtime_GenericAttachment_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:

+  [AWS SDK for C\+\+](http://docs.aws.amazon.com/goto/SdkForCpp/runtime.lex-2016-11-28/GenericAttachment) 

+  [AWS SDK for Go](http://docs.aws.amazon.com/goto/SdkForGoV1/runtime.lex-2016-11-28/GenericAttachment) 

+  [AWS SDK for Java](http://docs.aws.amazon.com/goto/SdkForJava/runtime.lex-2016-11-28/GenericAttachment) 

+  [AWS SDK for Ruby V2](http://docs.aws.amazon.com/goto/SdkForRubyV2/runtime.lex-2016-11-28/GenericAttachment) 