# Message<a name="API_Message"></a>

The message object that provides the message text and its type\.

## Contents<a name="API_Message_Contents"></a>

 **content**   
The text of the message\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 1000\.  
Required: Yes

 **contentType**   
The content type of the message string\.  
Type: String  
Valid Values:` PlainText | SSML | CustomPayload`   
Required: Yes

 **groupNumber**   
Identifies the message group that the message belongs to\. When a group is assigned to a message, Amazon Lex returns one message from each group in the response\.  
Type: Integer  
Valid Range: Minimum value of 1\. Maximum value of 5\.  
Required: No

## See Also<a name="API_Message_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:

+  [AWS SDK for C\+\+](http://docs.aws.amazon.com/goto/SdkForCpp/lex-models-2017-04-19/Message) 

+  [AWS SDK for Go](http://docs.aws.amazon.com/goto/SdkForGoV1/lex-models-2017-04-19/Message) 

+  [AWS SDK for Java](http://docs.aws.amazon.com/goto/SdkForJava/lex-models-2017-04-19/Message) 

+  [AWS SDK for Ruby V2](http://docs.aws.amazon.com/goto/SdkForRubyV2/lex-models-2017-04-19/Message) 