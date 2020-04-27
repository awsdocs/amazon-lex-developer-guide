# CodeHook<a name="API_CodeHook"></a>

Specifies a Lambda function that verifies requests to a bot or fulfills the user's request to a bot\.\.

## Contents<a name="API_CodeHook_Contents"></a>

 **messageVersion**   <a name="lex-Type-CodeHook-messageVersion"></a>
The version of the request\-response that you want Amazon Lex to use to invoke your Lambda function\. For more information, see [Using Lambda Functions](using-lambda.md)\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 5\.  
Required: Yes

 **uri**   <a name="lex-Type-CodeHook-uri"></a>
The Amazon Resource Name \(ARN\) of the Lambda function\.  
Type: String  
Length Constraints: Minimum length of 20\. Maximum length of 2048\.  
Pattern: `arn:aws:lambda:[a-z]+-[a-z]+-[0-9]:[0-9]{12}:function:[a-zA-Z0-9-_]+(/[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12})?(:[a-zA-Z0-9-_]+)?`   
Required: Yes

## See Also<a name="API_CodeHook_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/lex-models-2017-04-19/CodeHook) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/lex-models-2017-04-19/CodeHook) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/lex-models-2017-04-19/CodeHook) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/lex-models-2017-04-19/CodeHook) 