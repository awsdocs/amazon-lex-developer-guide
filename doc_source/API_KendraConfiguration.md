# KendraConfiguration<a name="API_KendraConfiguration"></a>

Provides configuration information for the AMAZON\.KendraSearchIntent intent\. When you use this intent, Amazon Lex searches the specified Amazon Kendra index and returns documents from the index that match the user's utterance\. For more information, see [ AMAZON\.KendraSearchIntent](http://docs.aws.amazon.com/lex/latest/dg/built-in-intent-kendra-search.html)\.

## Contents<a name="API_KendraConfiguration_Contents"></a>

 **kendraIndex**   <a name="lex-Type-KendraConfiguration-kendraIndex"></a>
The Amazon Resource Name \(ARN\) of the Amazon Kendra index that you want the AMAZON\.KendraSearchIntent intent to search\. The index must be in the same account and Region as the Amazon Lex bot\. If the Amazon Kendra index does not exist, you get an exception when you call the `PutIntent` operation\.  
Type: String  
Length Constraints: Minimum length of 20\. Maximum length of 2048\.  
Pattern: `arn:aws:kendra:[a-z]+-[a-z]+-[0-9]:[0-9]{12}:index\/[a-zA-Z0-9][a-zA-Z0-9_-]*`   
Required: Yes

 **queryFilterString**   <a name="lex-Type-KendraConfiguration-queryFilterString"></a>
A query filter that Amazon Lex sends to Amazon Kendra to filter the response from the query\. The filter is in the format defined by Amazon Kendra\. For more information, see [Filtering queries](http://docs.aws.amazon.com/kendra/latest/dg/filtering.html)\.  
You can override this filter string with a new filter string at runtime\.  
Type: String  
Length Constraints: Minimum length of 0\.  
Required: No

 **role**   <a name="lex-Type-KendraConfiguration-role"></a>
The Amazon Resource Name \(ARN\) of an IAM role that has permission to search the Amazon Kendra index\. The role must be in the same account and Region as the Amazon Lex bot\. If the role does not exist, you get an exception when you call the `PutIntent` operation\.  
Type: String  
Length Constraints: Minimum length of 20\. Maximum length of 2048\.  
Pattern: `arn:aws:iam::[0-9]{12}:role/.*`   
Required: Yes

## See Also<a name="API_KendraConfiguration_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/lex-models-2017-04-19/KendraConfiguration) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/lex-models-2017-04-19/KendraConfiguration) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/lex-models-2017-04-19/KendraConfiguration) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/lex-models-2017-04-19/KendraConfiguration) 