# Exporting to an Alexa Skill<a name="export-to-alexa"></a>

You can export your bot schema in a format compatible with an Alexa skill\. After you export the bot to a JSON file, you upload it to Alexa using the skill builder\.

**To export a bot and its schema \(interaction model\)**

1. Sign in to the AWS Management Console and open the Amazon Lex console at [https://console\.aws\.amazon\.com/lex/](https://console.aws.amazon.com/lex/)\.

1. For **Actions**, choose **Export**\.

1. Choose the name and version of the bot that you want to export\. For the format, choose **Alexa Skills Kit**, then choose **Export**\. 

1. When the download dialog box appears, choose a location to save the file, then choose **Save**\.

The downloaded file is a \.zip archive containing one file with the name of the exported bot\. It contains the information necessary to import the bot as an Alexa skill\.

**Note**  
Amazon Lex and the Alexa Skills Kit differ in the following ways:  
Session attributes, denoted by square brackets \(\[\]\), are not supported by the Alexa Skills Kit\. You need to update prompts that use session attributes\.
Punctuation marks are not supported by the Alexa Skills Kit\. You need to update utterances that use punctuation\.

**To upload the bot to an Alexa Skill**

1. Log in to the [Alexa Developer Console](https://developer.amazon.com/alexa/console/ask)\. 

2. Click the **Create Skill** Button\.

3. Define the *Skill Name* and click the **Next** button\.

4. Chose **Custom** for the model and click the **Create Skill** button\.

<p align="center"><img width='500px' src="https://m.media-amazon.com/images/G/01/mobile-apps/dex/ask-devconsole/choose-ia-model._TTH_.png" ></p>

5. On the left menu, select **Invocation**\.

6. Define the *Skill Invocation Name* and click **Save Model**\.

7. On the left menu, select **JSON Editor**\.

8. Extract the JSON file from the \.zip archive that you downloaded\. Drag and Drop the .json file or paste the contents of the JSON file into the code editor\.

9. Click **Save Model**, then Click **Build Model**\.

Complete the remaining items in the *Skill builder checklist*.

<p align="center"><img width='500px' src="https://m.media-amazon.com/images/G/01/mobile-apps/dex/ask-devconsole/skill-builder-checklist._TTH_.png" ></p>

For more information about creating an Alexa skill, see [Create a Skill and Choose the Interaction Model](https://developer.amazon.com/docs/devconsole/create-a-skill-and-choose-the-interaction-model.html)\. 
