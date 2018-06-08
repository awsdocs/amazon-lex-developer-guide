# Step 3: Integrate the Kik Bot with the Amazon Lex Bot<a name="kik-bot-assoc-create-assoc"></a>

Now that you have created an Amazon Lex bot and a Kik bot, you are ready to create an channel association between them in Amazon Lex\. When the association is activated, Amazon Lex automatically sets up a callback URL with Kik\.

1. Sign in to the AWS Management Console, and open the Amazon Lex console at [https://console\.aws\.amazon\.com/lex/](https://console.aws.amazon.com/lex/)\. 

1. Choose the Amazon Lex bot that you created in Step 1\.

1. Choose the **Channels** tab\.

1. In the **Channels** section, choose **Kik**\. 

1. On the Kik page, provide the following:
   + Type a name\. For example, `BotKikIntegration`\.
   + Type a description\.
   + Choose "aws/lex" from the **KMS key** drop\-down\.
   + For **Alias**, choose an alias from the drop\-down\.
   + For **Kik bot user name**, type the name that you gave the bot on Kik\.
   + For **Kik API key**, type the API key that was assigned to the bot on Kik\.
   + For **User greeting**, type the greeting that you would like your bot to send the first time that a user chats with it\.
   + For **Error message**, enter an error message that is shown to the user when part of the conversation is not understood\.
   + For **Group chat behavior**, choose one of the options:
     + **Enable** – Enables the entire chat group to interact with your bot in a single conversation\.
     + **Disable** – Restricts the conversation to one user in the chat group\.

        
![\[The Kik configuration screen.\]](http://docs.aws.amazon.com/lex/latest/dg/images/kik-10.png)
   + Choose **Activate** to create the association and link it to the Kik bot\.

**Next Step**  
[Step 4: Test the Integration](kik-bot-assoc-test.md)