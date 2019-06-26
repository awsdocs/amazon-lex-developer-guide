# Step 1: Create an Amazon Lex Bot \(Console\)<a name="gs-bp-create-bot"></a>

For this exercise, create a bot for ordering flowers, called OrderFlowersBot\.

To create an Amazon Lex bot \(console\)

1. Sign in to the AWS Management Console and open the Amazon Lex console at [https://console\.aws\.amazon\.com/lex/](https://console.aws.amazon.com/lex/)\.

1. If this is your first bot, choose **Get Started**; otherwise, on the **Bots** page, choose **Create**\. 

1. On the **Create your Lex bot** page, provide the following information, and then choose **Create**\.
   + Choose the **OrderFlowers** blueprint\.
   + Leave the default bot name \(OrderFlowers\)\.
   + For **COPPA**, choose **No**\.

1. Choose **Create**\. The console makes the necessary requests to Amazon Lex to save the configuration\. The console then displays the bot editor window\.

1. Wait for confirmation that your bot was built\.

1. Test the bot\.
**Note**  
You can test the bot by typing text into the test window, or, for compatible browsers, by choosing the microphone button in the test window and speaking\. 

   Use the following example text to engage in conversation with the bot to order flowers:  
![\[\]](http://docs.aws.amazon.com/lex/latest/dg/images/OrderFlowers-NoLambda.png)

   From this input, the bot infers the `OrderFlowers` intent and prompts for slot data\. When you provide all of the required slot data, the bot fulfills the intent \(`OrderFlowers`\) by returning all of the information to the client application \(in this case, the console\)\. The console shows the information in the test window\.

   Specifically:
   + In the statement "What day do you want the roses to be picked up?,"the term "roses" appears because the prompt for the `pickupDate` slot is configured using substitutions, `{FlowerType}`\. Verify this in the console\.
   + The "Okay, your roses will be ready\.\.\." statement is the confirmation prompt that you configured\. 
   + The last statement \("`FlowerType:roses...`"\) is just the slot data that is returned to the client, in this case, in the test window\. In the next exercise, you use a Lambda function to fulfill the intent, in which case you get a message indicating that the order is fulfilled\.

**Next Step**  
[Step 2 \(Optional\): Review the Details of Information Flow \(Console\)](gs-bp-details-two-runtime-apis.md)