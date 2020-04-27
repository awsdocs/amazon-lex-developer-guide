# SentimentResponse<a name="API_runtime_SentimentResponse"></a>

The sentiment expressed in an utterance\.

When the bot is configured to send utterances to Amazon Comprehend for sentiment analysis, this field structure contains the result of the analysis\.

## Contents<a name="API_runtime_SentimentResponse_Contents"></a>

 **sentimentLabel**   <a name="lex-Type-runtime_SentimentResponse-sentimentLabel"></a>
The inferred sentiment that Amazon Comprehend has the highest confidence in\.  
Type: String  
Required: No

 **sentimentScore**   <a name="lex-Type-runtime_SentimentResponse-sentimentScore"></a>
The likelihood that the sentiment was correctly inferred\.  
Type: String  
Required: No

## See Also<a name="API_runtime_SentimentResponse_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/runtime.lex-2016-11-28/SentimentResponse) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/runtime.lex-2016-11-28/SentimentResponse) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/runtime.lex-2016-11-28/SentimentResponse) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/runtime.lex-2016-11-28/SentimentResponse) 