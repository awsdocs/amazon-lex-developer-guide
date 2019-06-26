# Step 2: Set Up the AWS Command Line Interface<a name="gs-set-up-cli"></a>

If you prefer to use Amazon Lex with the AWS Command Line Interface \(AWS CLI\), download and configure it\.

**Important**  
You don't need the AWS CLI to perform the steps in the Getting Started exercises\. However, some of the later exercises in this guide use the AWS CLI\. If you prefer to start by using the console, skip this step and go to [Step 3: Getting Started \(Console\)](gs-console.md)\. Later, when you need the AWS CLI, return here to set it up\.

**To set up the AWS CLI**

1. Download and configure the AWS CLI\. For instructions, see the following topics in the *AWS Command Line Interface User Guide*: 
   + [Getting Set Up with the AWS Command Line Interface](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-set-up.html)
   + [Configuring the AWS Command Line Interface](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html)

1. Add a named profile for the administrator user to the end of the AWS CLI config file\. You use this profile when executing AWS CLI commands\. For more information about named profiles, see [Named Profiles](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html#cli-multiple-profiles) in the *AWS Command Line Interface User Guide*\.

   ```
   [profile adminuser]
   aws_access_key_id = adminuser access key ID
   aws_secret_access_key = adminuser secret access key
   region = aws-region
   ```

   For a list of available AWS Regions, see [Regions and Endpoints](https://docs.aws.amazon.com/general/latest/gr/rande.html) in the *Amazon Web Services General Reference*\.

1. Verify the setup by typing the Help command at the command prompt: 

   ```
   aws help
   ```

## <a name="gs-next-step-3"></a>

[Step 3: Getting Started \(Console\)](gs-console.md)