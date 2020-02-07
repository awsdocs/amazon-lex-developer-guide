# Exercise 6: Clean Up \(AWS CLI\)<a name="gs-cli-clean-up"></a>

Delete the resources that you created and clean up your account\.

You can delete only resources that are not in use\. In general, you should delete resources in the following order\.

1. Delete aliases to free up bot resources\.

1. Delete bots to free up intent resources\.

1. Delete intents to free up slot type resources\.

1. Delete slot types\.

To run the commands in this exercise, you need to know the region where the commands will be run\. For a list of regions, see [ Model Building Quotas ](gl-limits.md#gl-limits-model-building)\.

**To clean up your account \(AWS CLI\)**

1. In the AWS CLI command line, delete the alias:

   ```
   aws lex-models delete-bot-alias \
       --region region \
       --name PROD \
       --bot-name OrderFlowersBot
   ```

1. In the AWS CLI command line, delete the bot:

   ```
   aws lex-models delete-bot \
       --region region \
       --name OrderFlowersBot
   ```

1. In the AWS CLI command line, delete the intent:

   ```
   aws lex-models delete-intent \
       --region region \
       --name OrderFlowers
   ```

1. From the AWS CLI command line, delete the slot type:

   ```
   aws lex-models delete-slot-type \
       --region region \
       --name FlowerTypes
   ```

You have removed all of the resources that you created and cleaned up your account\.