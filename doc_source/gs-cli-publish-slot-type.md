# Step 1: Publish the Slot Type \(AWS CLI\)<a name="gs-cli-publish-slot-type"></a>

Before you can publish a version of any intents that use a slot type, you must publish a version of that slot type\. In this case, you publish the `FlowerTypes` slot type\. 

**Note**  
The following AWS CLI example is formatted for Unix, Linux, and macOS\. For Windows, change `"\$LATEST"` to `$LATEST` and replace the backslash \(\\\) continuation character at the end of each line with a caret \(^\)\.

**To publish a slot type \(AWS CLI\)**

1. In the AWS CLI, get the latest version of the slot type:

   ```
   aws lex-models get-slot-type \
       --region region \
       --name FlowerTypes \
       --slot-type-version "\$LATEST"
   ```

   The response from Amazon Lex follows\. Record the checksum for the current revision of the `$LATEST` version\.

   ```
   {
       "enumerationValues": [
           {
               "value": "tulips"
           }, 
           {
               "value": "lilies"
           }, 
           {
               "value": "roses"
           }
       ], 
       "name": "FlowerTypes", 
       "checksum": "checksum", 
       "version": "$LATEST", 
       "lastUpdatedDate": timestamp, 
       "createdDate": timestamp, 
       "description": "Types of flowers to pick up"
   }
   ```

1. Publish a version of the slot type\. Use the checksum that you recorded in the previous step\.

   ```
   aws lex-models create-slot-type-version \
       --region region \
       --name FlowerTypes \
       --checksum "checksum"
   ```

   The response from Amazon Lex follows\. Record the version number for the next step\.

   ```
   {
       "version": "1", 
       "enumerationValues": [
           {
               "value": "tulips"
           }, 
           {
               "value": "lilies"
           }, 
           {
               "value": "roses"
           }
       ], 
       "name": "FlowerTypes", 
       "createdDate": timestamp, 
       "lastUpdatedDate": timestamp, 
       "description": "Types of flowers to pick up"
   }
   ```

## Next Step<a name="gs-cli-publish-2"></a>

[Step 2: Publish the Intent \(AWS CLI\)](gs-cli-publish-intent.md)