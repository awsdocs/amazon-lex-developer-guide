# Step 3: Create an Intent \(AWS CLI\)<a name="gs-cli-create-order-flowers"></a>

Create an intent for the `OrderFlowersBot` bot and provide three slots, or parameters\. The slots allow the bot to fulfill the intent:
+ `FlowerType` is a custom slot type that specifies which types of flowers can be ordered\.
+ `AMAZON.DATE` and `AMAZON.TIME` are built\-in slot types used for getting the date and time to deliver the flowers from the user\.

To run the commands in this exercise, you need to know the region where the commands will be run\. For a list of regions, see [ Model Building Quotas ](gl-limits.md#gl-limits-model-building)\.

**To create the `OrderFlowers` intent \(AWS CLI\)**

1. Create a text file named **OrderFlowers\.json**\. Copy the JSON code from [OrderFlowers\.json](gs-cli-create-order-flowers-json.md) into the text file\.

1. In the AWS CLI, call the [PutIntent](API_PutIntent.md) operation to create the intent\. The example is formatted for Unix, Linux, and macOS\. For Windows, replace the backslash \(\\\) Unix continuation character at the end of each line with a caret \(^\)\.

   ```
   aws lex-models put-intent \
      --region region \
      --name OrderFlowers \
      --cli-input-json file://OrderFlowers.json
   ```

   The server responds with the following:

   ```
   {
       "confirmationPrompt": {
           "maxAttempts": 2, 
           "messages": [
               {
                   "content": "Okay, your {FlowerType} will be ready for pickup by {PickupTime} on {PickupDate}.  Does this sound okay?", 
                   "contentType": "PlainText"
               }
           ]
       }, 
       "name": "OrderFlowers", 
       "checksum": "checksum", 
       "version": "$LATEST", 
       "rejectionStatement": {
           "messages": [
               {
                   "content": "Okay, I will not place your order.", 
                   "contentType": "PlainText"
               }
           ]
       }, 
       "createdDate": timestamp, 
       "lastUpdatedDate": timestamp, 
       "sampleUtterances": [
           "I would like to pick up flowers", 
           "I would like to order some flowers"
       ], 
       "slots": [
           {
               "slotType": "AMAZON.TIME", 
               "name": "PickupTime", 
               "slotConstraint": "Required", 
               "valueElicitationPrompt": {
                   "maxAttempts": 2, 
                   "messages": [
                       {
                           "content": "Pick up the {FlowerType} at what time on {PickupDate}?", 
                           "contentType": "PlainText"
                       }
                   ]
               }, 
               "priority": 3, 
               "description": "The time to pick up the flowers"
           }, 
           {
               "slotType": "FlowerTypes", 
               "name": "FlowerType", 
               "slotConstraint": "Required", 
               "valueElicitationPrompt": {
                   "maxAttempts": 2, 
                   "messages": [
                       {
                           "content": "What type of flowers would you like to order?", 
                           "contentType": "PlainText"
                       }
                   ]
               }, 
               "priority": 1, 
               "slotTypeVersion": "$LATEST", 
               "sampleUtterances": [
                   "I would like to order {FlowerType}"
               ], 
               "description": "The type of flowers to pick up"
           }, 
           {
               "slotType": "AMAZON.DATE", 
               "name": "PickupDate", 
               "slotConstraint": "Required", 
               "valueElicitationPrompt": {
                   "maxAttempts": 2, 
                   "messages": [
                       {
                           "content": "What day do you want the {FlowerType} to be picked up?", 
                           "contentType": "PlainText"
                       }
                   ]
               }, 
               "priority": 2, 
               "description": "The date to pick up the flowers"
           }
       ], 
       "fulfillmentActivity": {
           "type": "ReturnIntent"
       }, 
       "description": "Intent to order a bouquet of flowers for pick up"
   }
   ```

## Next Step<a name="gs-create-next-4"></a>

[Step 4: Create a Bot \(AWS CLI\)](gs-cli-create-order-flowers-bot.md)