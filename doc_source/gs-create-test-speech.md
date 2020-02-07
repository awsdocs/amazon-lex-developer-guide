# Test the Bot Using Speech Input \(AWS CLI\)<a name="gs-create-test-speech"></a>

To test the bot using audio files, use the [PostContent](API_runtime_PostContent.md) operation\. You generate the audio files using Amazon Polly text\-to\-speech operations\.

To run the commands in this exercise, you need to know the region the Amazon Lex and Amazon Polly commands will be run\. For a list of regions for Amazon Lex, see [Runtime Service Quotas](gl-limits.md#gl-limits-runtime)\. For a list of regions for Amazon Polly see [ AWS Regions and Endpoints ](https://docs.aws.amazon.com/general/latest/gr/rande.html#pol_region) in the *Amazon Web Services General Reference*\.

**Note**  
The following AWS CLI example is formatted for Unix, Linux, and macOS\. For Windows, change `"\$LATEST"` to `$LATEST` and replace the backslash \(\\\) continuation character at the end of each line with a caret \(^\)\.

**To use a speech input to test the bot \(AWS CLI\)**

1. In the AWS CLI, create an audio file using Amazon Polly\. The example is formatted for Unix, Linux, and macOS\. For Windows, replace the backslash \(\\\) Unix continuation character at the end of each line with a caret \(^\)\.

   ```
   aws polly synthesize-speech \
       --region region \
       --output-format pcm \
       --text "i would like to order flowers" \
       --voice-id "Salli" \
       IntentSpeech.mpg
   ```

1. To send the audio file to Amazon Lex, run the following command\. Amazon Lex saves the audio from the response in the specified output file\. 

   ```
   aws lex-runtime post-content \
       --region region \
       --bot-name OrderFlowersBot \
       --bot-alias "\$LATEST" \
       --user-id UserOne \
       --content-type "audio/l16; rate=16000; channels=1" \
       --input-stream IntentSpeech.mpg \
       IntentOutputSpeech.mpg
   ```

   Amazon Lex responds with a request for the first slot\. It saves the audio response in the specified output file\.

   ```
   {
       "contentType": "audio/mpeg", 
       "slotToElicit": "FlowerType", 
       "dialogState": "ElicitSlot", 
       "intentName": "OrderFlowers", 
       "inputTranscript": "i would like to order some flowers", 
       "slots": {
           "PickupDate": null, 
           "PickupTime": null, 
           "FlowerType": null
       }, 
       "message": "What type of flowers would you like to order?"
   }
   ```

1. To order roses, create the following audio file and send it to Amazon Lex :

   ```
   aws polly synthesize-speech \
       --region region \
       --output-format pcm \
       --text "roses" \
       --voice-id "Salli" \ 
       FlowerTypeSpeech.mpg
   ```

   ```
   aws lex-runtime post-content \
       --region region \
       --bot-name OrderFlowersBot \
       --bot-alias "\$LATEST" \
       --user-id UserOne \
       --content-type "audio/l16; rate=16000; channels=1" \
       --input-stream FlowerTypeSpeech.mpg \
       FlowerTypeOutputSpeech.mpg
   ```

1. To set the delivery date, create the following audio file and send it to Amazon Lex:

   ```
   aws polly synthesize-speech \
       --region region \
       --output-format pcm \
       --text "tuesday" \
       --voice-id "Salli" \ 
       DateSpeech.mpg
   ```

   ```
   aws lex-runtime post-content \
       --region region \
       --bot-name OrderFlowersBot \
       --bot-alias "\$LATEST" \
       --user-id UserOne \
       --content-type "audio/l16; rate=16000; channels=1" \
       --input-stream DateSpeech.mpg \
       DateOutputSpeech.mpg
   ```

1. To set the delivery time, create the following audio file and send it to Amazon Lex:

   ```
   aws polly synthesize-speech \
       --region region \
       --output-format pcm \
       --text "10:00 a.m." \
       --voice-id "Salli" \
       TimeSpeech.mpg
   ```

   ```
   aws lex-runtime post-content \
       --region region \
       --bot-name OrderFlowersBot \
       --bot-alias "\$LATEST" \
       --user-id UserOne \
       --content-type "audio/l16; rate=16000; channels=1" \
       --input-stream TimeSpeech.mpg \
       TimeOutputSpeech.mpg
   ```

1. To confirm the delivery, create the following audio file and send it to Amazon Lex:

   ```
   aws polly synthesize-speech \
       --region region \
       --output-format pcm \
       --text "yes" \
       --voice-id "Salli" \
       ConfirmSpeech.mpg
   ```

   ```
   aws lex-runtime post-content \
       --region region \
       --bot-name OrderFlowersBot \
       --bot-alias "\$LATEST" \
       --user-id UserOne \
       --content-type "audio/l16; rate=16000; channels=1" \
       --input-stream ConfirmSpeech.mpg \
       ConfirmOutputSpeech.mpg
   ```

   After you confirm the delivery, Amazon Lex sends a response that confirms fulfillment of the intent: 

   ```
   {
       "contentType": "text/plain;charset=utf-8", 
       "dialogState": "ReadyForFulfillment", 
       "intentName": "OrderFlowers", 
       "inputTranscript": "yes", 
       "slots": {
           "PickupDate": "2017-05-16", 
           "PickupTime": "10:00", 
           "FlowerType": "roses"
       }
   }
   ```

## Next Step<a name="gs-cli-next-exercise-2"></a>

[Exercise 2: Add a New Utterance \(AWS CLI\)](gs-cli-update-utterance.md)