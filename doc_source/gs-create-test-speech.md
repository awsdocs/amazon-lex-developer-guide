# Test the Bot Using Speech Input \(AWS CLI\)<a name="gs-create-test-speech"></a>

To test the bot using audio files, use the [PostContent](API_runtime_PostContent.md) operation\. You generate the audio files using Amazon Polly text\-to\-speech operations\.

**Note**  
The following AWS CLI example is formatted for Unix, Linux, and macOS\. For Windows, change `"\$LATEST"` to `$LATEST`\.

**To use a speech input to test the bot \(AWS CLI\)**

1. In the AWS CLI, create an audio file using Amazon Polly\. The example is formatted for Unix, Linux, and macOS\. For Windows, replace the backslash \(\\\) Unix continuation character at the end of each line with a caret \(^\)\.

   ```
   aws polly synthesize-speech \
       --region region \
       --endpoint endpoint \                        
       --output-format pcm \
       --text "i would like to order flowers" \
       --voice-id "Kendra" \
       IntentSpeech.mpg
   ```

1. To send the audio file to Amazon Lex, run the following command\. Amazon Lex saves the audio from the response in the specified output file\. 

   ```
   aws lex-runtime post-content 
       --region region \
       --endpoint endpoint \                            
       --bot-name OrderFlowersBot \
       --bot-alias "\$LATEST" \
       --user-id UserOne \
       --content-type "audio/l16; rate=16000; channels=1" \
       --input-stream IntentSpeech.mpg \
       IntentOutputSpeech.mpg
   ```

   Amazon Lex responds with a request for the first slot\. It saves the audio response in the specified output file\.

1. To set the appointment type, create the following audio file and send it to Amazon Lex :

   ```
   aws polly synthesize-speech \
       --region region \
       --endpoint endpoint \     
       --output-format pcm \
       --text "roses" \
       --voice-id "Kendra" 
       FlowerTypeSpeech.mpg
   ```

   ```
   aws lex-runtime post-content \
       --region region \
       --endpoint endpoint \     
       --bot-name OrderFlowersBot \
       --bot-alias "\$LATEST" \
       --user-id UserOne \
       --content-type "audio/l16; rate=16000; channels=1" \
       --input-stream FlowerTypeSpeech.mpg \
       FlowerTypeOutputSpeech.mpg
   ```

1. To set the appointment date, create the following audio file and send it to Amazon Lex:

   ```
   aws polly synthesize-speech \
       --region region \
       --endpoint endpoint \     
       --output-format pcm \
       --text "tuesday" \
       --voice-id "Kendra" 
       DateSpeech.mpg
   ```

   ```
   aws lex-runtime post-content \
       --region region \
       --endpoint endpoint \     
       --bot-name OrderFlowersBot \
       --bot-alias "\$LATEST" \
       --user-id UserOne \
       --content-type "audio/l16; rate=16000; channels=1" \
       --input-stream DateSpeech.mpg 
       DateOutputSpeech.mpg
   ```

1. To set the appointment time, create the following audio file and send it to Amazon Lex:

   ```
   aws polly synthesize-speech \
       --region region \
       --endpoint endpoint \     
       --output-format pcm \
       --text "10:00 a.m." \
       --voice-id "Kendra" 
       TimeSpeech.mpg
   ```

   ```
   aws lex-runtime post-content \
       --region region \
       --endpoint endpoint \     
       --bot-name OrderFlowersBot \
       --bot-alias "\$LATEST" \
       --user-id UserOne \
       --content-type "audio/l16; rate=16000; channels=1" \
       --input-stream TimeSpeech.mpg 
       TimeOutputSpeech.mpg
   ```

1. To confirm the appointment, create the following audio file and send it to Amazon Lex:

   ```
   aws polly synthesize-speech \
       --region region \
       --endpoint endpoint \     
       --output-format pcm \
       --text "yes" \
       --voice-id "Kendra" 
       ConfirmSpeech.mpg
   ```

   ```
   aws lex-runtime post-content \
       --region region \
       --endpoint endpoint \     
       --bot-name OrderFlowersBot \
       --bot-alias "\$LATEST" \
       --user-id UserOne \
       --content-type "audio/l16; rate=16000; channels=1" \
       --input-stream ConfirmSpeech.mpg \
       ConfirmOutputSpeech.mpg
   ```

   After you confirm the appointment, Amazon Lex sends a response that confirms fulfillment of the intent: 

## Next Step<a name="gs-cli-next-exercise-2"></a>

[Exercise 2: Add a New Utterance \(AWS CLI\)](gs-cli-update-utterance.md)