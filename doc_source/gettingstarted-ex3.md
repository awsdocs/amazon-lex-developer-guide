# Exercise 3: Publish a Version and Create an Alias<a name="gettingstarted-ex3"></a>

In Getting Started Exercises 1 and 2, you created a bot and tested it\. In this exercise, you do the following:
+ Publish a new version of the bot\. Amazon Lex takes a snapshot copy of the `$LATEST` version to publish a new version\. 
+ Create an alias that points to the new version\. 

For more information about versioning and aliases, see [Versioning and Aliases](versioning-aliases.md)\.

Do the following to publish a version of a bot you created for this exercise:

1. In the Amazon Lex console, choose one of the bots you created\. 

   Verify that the console shows the `$LATEST` as the bot version next to the bot name\.

1. Choose **Publish**\.

1. On the **Publish *botname*** wizard, specify the alias **BETA**, and then choose **Publish**\.

1. Verify that the Amazon Lex console shows the new version next to the bot name\.   
![\[\]](http://docs.aws.amazon.com/lex/latest/dg/images/gs2-final.png)

Now that you have a working bot with published version and an alias, you can deploy the bot \(in your mobile application or integrate the bot with Facebook Messenger\)\. For an example, see [Integrating an Amazon Lex Bot with Facebook Messenger](fb-bot-association.md)\.