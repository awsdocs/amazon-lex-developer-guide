# Step 3: Publish the Bot \(AWS CLI\)<a name="gs-cli-publish-bot"></a>

After you have published all of the slot types and intents that are used by your bot, you can publish the bot\.

Update the `OrderFlowersBot` bot to use the `OrderFlowers` intent that you updated in the previous step\. Then, publish a new version of the `OrderFlowersBot` bot\.

**Note**  
The following AWS CLI example is formatted for Unix, Linux, and macOS\. For Windows, change `"\$LATEST"` to `$LATEST` and replace the backslash \(\\\) continuation character at the end of each line with a caret \(^\)\.

**To publish a version of a bot \(AWS CLI\)**

1. In the AWS CLI, get the `$LATEST` version of the `OrderFlowersBot` bot and save it to a file:

   ```
   aws lex-models get-bot \
       --region region \
       --name OrderFlowersBot \
       --version-or-alias "\$LATEST" > OrderFlowersBot_V4.json
   ```

1. In a text editor, open the **OrderFlowersBot\_V4\.json** file\. Delete the `createdDate`, `lastUpdatedDate`, `status` and `version` fields\. Find the `OrderFlowers` intent and change the version to the version number that you recorded in the previous step\. The following fragment of **OrderFlowersBot\_V4\.json** shows the location of the change\.

   ```
       "intents": [
           {
               "intentVersion": "version", 
               "intentName": "OrderFlowers"
           }
   ```

1. In the AWS CLI, save the new revision of the bot\. Make note of the version number returned by the call to `put-bot`\.

   ```
   aws lex-models put-bot \
       --name OrderFlowersBot \
       --cli-input-json file://OrderFlowersBot_V4.json
   ```

1. Get the checksum of the latest revision of the bot\. Use the version number returned in step 3\.

   ```
   aws lex-models get-bot \
       --region region \
       --version-or-alias version \
       --name OrderFlowersBot > OrderFlowersBot_V4a.json
   ```

   The following fragment of the response shows the checksum of the bot\. Record this for the next step\.

   ```
       "name": "OrderFlowersBot", 
       "locale": "en-US", 
       "checksum": "checksum",
   ```

1. Publish a new version of the bot:

   ```
   aws lex-models create-bot-version \
       --region region \
       --name OrderFlowersBot \
       --checksum "checksum"
   ```

   The following fragment of the response shows the new version of the bot\.

   ```
       "checksum": "checksum", 
       "abortStatement": {
           ...
       }, 
       "version": "1",
       "lastUpdatedDate": timestamp,
   ```

## Next Step<a name="gs-cli-next-exercise-5"></a>

[Exercise 5: Create an Alias \(AWS CLI\)](gs-cli-create-alias.md)