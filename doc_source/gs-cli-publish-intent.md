# Step 2: Publish the Intent \(AWS CLI\)<a name="gs-cli-publish-intent"></a>

Before you can publish an intent, you have to publish all of the slot types referred to by the intent\. The slot types must be numbered versions, not the `$LATEST` version\.

First, update the `OrderFlowers` intent to use the version of the `FlowerTypes` slot type that you published in the previous step\. Then publish a new version of the `OrderFlowers` intent\.

**Note**  
The following AWS CLI example is formatted for Unix, Linux, and macOS\. For Windows, change `"\$LATEST"` to `$LATEST` and replace the backslash \(\\\) continuation character at the end of each line with a caret \(^\)\.

**To publish a version of an intent \(AWS CLI\)**

1. In the AWS CLI, get the `$LATEST` version of the `OrderFlowers` intent and save it to a file:

   ```
   aws lex-models get-intent \
       --region region \
       --name OrderFlowers \
       --intent-version "\$LATEST" > OrderFlowers_V4.json
   ```

1. In a text editor, open the **OrderFlowers\_V4\.json** file\. Delete the `createdDate`, `lastUpdatedDate`, and `version` fields\. Find the `FlowerTypes` slot type and change the version to the version number that you recorded in the previous step\. The following fragment of the **OrderFlowers\_V4\.json** file shows the location of the change:

   ```
           {
               "slotType": "FlowerTypes", 
               "name": "FlowerType", 
               "slotConstraint": "Required", 
               "valueElicitationPrompt": {
                   "maxAttempts": 2, 
                   "messages": [
                       {
                           "content": "What type of flowers?", 
                           "contentType": "PlainText"
                       }
                   ]
               }, 
               "priority": 1, 
               "slotTypeVersion": "version", 
               "sampleUtterances": []
           },
   ```

1. In the AWS CLI, save the revision of the intent:

   ```
   aws lex-models put-intent \
       --name OrderFlowers \
       --cli-input-json file://OrderFlowers_V4.json
   ```

1. Get the checksum of the latest revision of the intent:

   ```
   aws lex-models get-intent \
       --region region \
       --name OrderFlowers \
       --intent-version "\$LATEST" > OrderFlowers_V4a.json
   ```

   The following fragment of the response shows the checksum of the intent\. Record this for the next step\.

   ```
       "name": "OrderFlowers", 
       "checksum": "checksum", 
       "version": "$LATEST",
   ```

1. Publish a new version of the intent: 

   ```
   aws lex-models create-intent-version \
       --region region \
       --name OrderFlowers \
       --checksum "checksum"
   ```

   The following fragment of the response shows the new version of the intent\. Record the version number for the next step\.

   ```
       "name": "OrderFlowers", 
       "checksum": "checksum", 
       "version": "version",
   ```

## Next Step<a name="gs-cli-publish-3"></a>

[Step 3: Publish the Bot \(AWS CLI\)](gs-cli-publish-bot.md)