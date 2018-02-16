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

1. Log in to the developer portal at [https://developer\.amazon\.com/](https://developer.amazon.com/edw/home.html#/)\. 

1. To open the Alexa console, choose **Developer Console**, then choose **ALEXA**\.

1. Open the Alexa Skill Kit page\. In the **Alexa Skills Kit** box, choose **Get Started**\. 

1. Choose **Add a New Skill**\. Fill in the required fields:

   + **Skill Type** \(choose **Custom Interaction Model**\)

   + **Language**

   + **Name**

   + **Invocation Name**

1. Choose **Save**, then choose **Next**\.

1. Choose **Launch Skill Builder**\.

1. On the left menu, choose **Code Editor**\.

1. Extract the JSON file from the \.zip archive that you downloaded\. Paste the contents of the JSON file into the code editor\.

1. Choose **Apply Changes**, then choose **Build Model**\.

After uploading the schema into the Alexa skill, make changes necessary for running the skill with Alexa\. For more information about creating an Alexa skill, see [Use the Skill Builder \(Beta\)](https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit/docs/ask-define-the-vui-with-gui) in the *Alexa Skills Kit*\. 