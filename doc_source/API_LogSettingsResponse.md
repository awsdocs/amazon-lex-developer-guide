# LogSettingsResponse<a name="API_LogSettingsResponse"></a>

The settings for conversation logs\.

## Contents<a name="API_LogSettingsResponse_Contents"></a>

 **destination**   <a name="lex-Type-LogSettingsResponse-destination"></a>
The destination where logs are delivered\.  
Type: String  
Valid Values:` CLOUDWATCH_LOGS | S3`   
Required: No

 **kmsKeyArn**   <a name="lex-Type-LogSettingsResponse-kmsKeyArn"></a>
The Amazon Resource Name \(ARN\) of the key used to encrypt audio logs in an S3 bucket\.  
Type: String  
Length Constraints: Minimum length of 20\. Maximum length of 2048\.  
Pattern: `^arn:[\w\-]+:kms:[\w\-]+:[\d]{12}:(?:key\/[\w\-]+|alias\/[a-zA-Z0-9:\/_\-]{1,256})$`   
Required: No

 **logType**   <a name="lex-Type-LogSettingsResponse-logType"></a>
The type of logging that is enabled\.  
Type: String  
Valid Values:` AUDIO | TEXT`   
Required: No

 **resourceArn**   <a name="lex-Type-LogSettingsResponse-resourceArn"></a>
The Amazon Resource Name \(ARN\) of the CloudWatch Logs log group or S3 bucket where the logs are delivered\.  
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 2048\.  
Pattern: `^arn:[\w\-]+:(?:logs:[\w\-]+:[\d]{12}:log-group:[\.\-_/#A-Za-z0-9]{1,512}(?::\*)?|s3:::[a-z0-9][\.\-a-z0-9]{1,61}[a-z0-9])$`   
Required: No

 **resourcePrefix**   <a name="lex-Type-LogSettingsResponse-resourcePrefix"></a>
The resource prefix is the first part of the S3 object key within the S3 bucket that you specified to contain audio logs\. For CloudWatch Logs it is the prefix of the log stream name within the log group that you specified\.   
Type: String  
Length Constraints: Maximum length of 1024\.  
Required: No

## See Also<a name="API_LogSettingsResponse_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:
+  [AWS SDK for C\+\+](https://docs.aws.amazon.com/goto/SdkForCpp/lex-models-2017-04-19/LogSettingsResponse) 
+  [AWS SDK for Go](https://docs.aws.amazon.com/goto/SdkForGoV1/lex-models-2017-04-19/LogSettingsResponse) 
+  [AWS SDK for Java](https://docs.aws.amazon.com/goto/SdkForJava/lex-models-2017-04-19/LogSettingsResponse) 
+  [AWS SDK for Ruby V3](https://docs.aws.amazon.com/goto/SdkForRubyV3/lex-models-2017-04-19/LogSettingsResponse) 