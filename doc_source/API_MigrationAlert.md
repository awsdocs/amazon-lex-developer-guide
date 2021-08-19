# MigrationAlert<a name="API_MigrationAlert"></a>

Provides information about alerts and warnings that Amazon Lex sends during a migration\. The alerts include information about how to resolve the issue\.

## Contents<a name="API_MigrationAlert_Contents"></a>

 **details**   <a name="lex-Type-MigrationAlert-details"></a>
Additional details about the alert\.  
Type: Array of strings  
Required: No

 **message**   <a name="lex-Type-MigrationAlert-message"></a>
A message that describes why the alert was issued\.  
Type: String  
Required: No

 **referenceURLs**   <a name="lex-Type-MigrationAlert-referenceURLs"></a>
A link to the Amazon Lex documentation that describes how to resolve the alert\.  
Type: Array of strings  
Required: No

 **type**   <a name="lex-Type-MigrationAlert-type"></a>
The type of alert\. There are two kinds of alerts:  
+  `ERROR` \- There was an issue with the migration that can't be resolved\. The migration stops\.
+  `WARN` \- There was an issue with the migration that requires manual changes to the new Amazon Lex V2 bot\. The migration continues\.
Type: String  
Valid Values:` ERROR | WARN`   
Required: No

## See Also<a name="API_MigrationAlert_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [ AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/lex-models-2017-04-19/MigrationAlert) 
+  [ AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/lex-models-2017-04-19/MigrationAlert) 
+  [ AWS SDK for Java V2](https://docs.aws.amazon.com/goto/SdkForJavaV2/lex-models-2017-04-19/MigrationAlert) 
+  [ AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/lex-models-2017-04-19/MigrationAlert) 