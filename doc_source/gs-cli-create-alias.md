# Exercise 5: Create an Alias \(AWS CLI\)<a name="gs-cli-create-alias"></a>

An alias is a pointer to a specific version of a bot\. With an alias you can easily update the version that your client applications are using\. For more information, see [Versioning and Aliases](versioning-aliases.md)

**To create an alias \(AWS CLI\)**

1. In the AWS CLI, get the version of the `OrderFlowersBot` bot that you created in [Exercise 4: Publish a Version \(AWS CLI\)](gs-cli-publish.md)\. 

   ```
   aws lex-models get-bot 
       --region region \
       --endpoint endpoint \     
       --name OrderFlowersBot \
       --version-or-alias version > OrderFlowersBot_V5.json
   ```

1. In a text editor, open **OrderFlowersBot\_v5\.json**\. Find and record the version number\.

1. In the AWS CLI, create the bot alias:

   ```
   aws lex-models put-bot-alias  \
       --region region \
       --endpoint endpoint \
       --name PROD \
       --bot-name OrderFlowersBot \
       --bot-version version
   ```

   The following is the reponse from the server:

## Next Step<a name="gs-cli-next-exercise-6"></a>

[Exercise 6: Clean Up \(AWS CLI\)](gs-cli-clean-up.md)