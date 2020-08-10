# Step 4: Set up Amazon Cognito<a name="agent-step-4"></a>

To manage permissions and users for the web application, you need to set up Amazon Cognito\. Amazon Cognito ensures that the web application is secure and has access control\. Amazon Cognito uses identity pools to provide AWS credentials that grant your users access to other AWS services\. For this tutorial, it provides access to Amazon Lex\.

When creating an identity pool, Amazon Cognito provides you with AWS Identity and Access Management \(IAM\) roles for authenticated and unauthenticated users\. You modify the IAM roles by adding policies that grant access to Amazon Lex\. 

**To set up Amazon Cognito**

1. Sign into the AWS Management Console and open the Amazon Cognito console at [https://console\.aws\.amazon\.com/cognito/](https://console.aws.amazon.com/cognito)\.

1. Choose **Manage Identity Pools**\.

1. Choose **Create new identity pool**\.

1. \.Configure the identity pool\.

   1. **Identity pool name** – Enter a name that indicates the pool's purpose, such as **BotPool**\.

   1. In the **Unauthenticated identities** section, choose **Enable access to unauthenticated identities**\.

1. Choose **Create Pool**\.

1. On the **Identify the IAM roles to use with your new identity pool** page, choose **View Details**\.

1. Record the IAM role names\. You will modify them later\.

1. Choose **Allow**\.

1. On the **Getting Started with Amazon Cognito** page, for **Platform**, choose **JavaScript**\.

1. In the **Get AWS Credentials** section, find and record the **Identity pool ID**\.

1. To allow access to Amazon Lex, modify the authenticated and unauthenticated IAM roles\.

   1. Sign in to the AWS Management Console and open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

   1. In the navigation pane, under **Access Management**, choose **Roles**\.

   1. In the search box, enter the name of the authenticated IAM role and choose the checkbox next to it\. 

      1. Choose **Attach policies**\.

      1. In the search box, enter **AmazonLexRunBotsOnly** and choose the checkbox next to it\.

      1. Choose **Attach policy**\.

   1. Enter the name of the unauthenticated IAM role in the search box and choose the checkbox next to it\. 

      1. Choose **Attach policies**\.

      1. In the search box, enter **AmazonLexRunBotsOnly** and choose the checkbox next to it\.

      1. Choose **Attach policy**\.

## Next step<a name="agent-step-4-next"></a>

[Step 5: Deploy Your Bot as a Web Application ](agent-step-5.md)