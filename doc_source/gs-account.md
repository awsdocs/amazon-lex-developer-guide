# Step 1: Set Up an AWS Account and Create an Administrator User<a name="gs-account"></a>

Before you use Amazon Lex for the first time, complete the following tasks: 

1. [Sign Up for AWS](#gs-account-create)

1. [Create an IAM User](#gs-account-user)

## Sign Up for AWS<a name="gs-account-create"></a>

If you already have an AWS account, skip this task\.

When you sign up for Amazon Web Services \(AWS\), your AWS account is automatically signed up for all services in AWS, including Amazon Lex\. You are charged only for the services that you use\.

With Amazon Lex, you pay only for the resources that you use\. If you are a new AWS customer, you can get started with Amazon Lex for free\. For more information, see [AWS Free Usage Tier](https://aws.amazon.com/free/)\.

If you already have an AWS account, skip to the next task\. If you don't have an AWS account, use the following procedure to create one\.

**To create an AWS account**

1. Open [https://portal\.aws\.amazon\.com/billing/signup](https://portal.aws.amazon.com/billing/signup)\.

1. Follow the online instructions\.

   Part of the sign\-up procedure involves receiving a phone call and entering a verification code on the phone keypad\.

Write down your AWS account ID because you'll need it for the next task\.

## Create an IAM User<a name="gs-account-user"></a>

Services in AWS, such as Amazon Lex, require that you provide credentials when you access them so that the service can determine whether you have permissions to access the resources owned by that service\. The console requires your password\. You can create access keys for your AWS account to access the AWS CLI or API\.

However, we don't recommend that you access AWS using the credentials for your AWS account\. Instead, we recommend that you:
+ Use AWS Identity and Access Management \(IAM\) to create an IAM user
+ Add the user to an IAM group with administrative permissions
+ Grant administrative permissions to the IAM user that you created\.

You can then access AWS using a special URL and the IAM user's credentials\.

The Getting Started exercises in this guide assume that you have a user \(`adminuser`\) with administrator privileges\. Follow the procedure to create `adminuser` in your account\.

**To create an administrator user and sign in to the console**

1. Create an administrator user called `adminuser` in your AWS account\. For instructions, see [Creating Your First IAM User and Administrators Group](https://docs.aws.amazon.com/IAM/latest/UserGuide/getting-started_create-admin-group.html) in the *IAM User Guide*\.

1. As a user, you can sign in to the AWS Management Console using a special URL\. For more information, [How Users Sign In to Your Account](https://docs.aws.amazon.com/IAM/latest/UserGuide/getting-started_how-users-sign-in.html) in the *IAM User Guide*\.

For more information about IAM, see the following:
+ [AWS Identity and Access Management \(IAM\)](https://aws.amazon.com/iam/)
+ [Getting Started](https://docs.aws.amazon.com/IAM/latest/UserGuide/getting-started.html)
+ [IAM User Guide](https://docs.aws.amazon.com/IAM/latest/UserGuide/)

## Next Step<a name="gs-next-step-2"></a>

[Step 2: Set Up the AWS Command Line Interface ](gs-set-up-cli.md)