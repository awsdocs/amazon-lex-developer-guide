# Step 1: Create an Amazon Lex Bot<a name="ex1-sch-appt-create-bot"></a>

In this section, you create an Amazon Lex bot using the ScheduleAppointment blueprint, which is provided in the Amazon Lex console\.

1. Sign in to the AWS Management Console and open the Amazon Lex console at [https://console\.aws\.amazon\.com/lex/](https://console.aws.amazon.com/lex/)\.

1. On the **Bots** page, choose **Create**\.

1. On the **Create your Lex bot** page, do the following:
   + Choose the **ScheduleAppointment** blueprint\.
   + Leave the default bot name \(ScheduleAppointment\)\.

1. Choose **Create**\.

   This step saves and builds the bot\. The console sends the following requests to Amazon Lex during the build process: 
   + Create a new version of the slot types \(from the $LATEST version\)\. For information about slot types defined in this bot blueprint, see [Overview of the Bot Blueprint \(ScheduleAppointment\)](ex1-sch-appt.md#ex1-sch-appt-bp-summary-bot)\.
   + Create a version of the `MakeAppointment` intent \(from the $LATEST version\)\. In some cases, the console sends a request for the `update` API operation before creating a new version\. 
   + Update the $LATEST version of the bot\. 

     At this time, Amazon Lex builds a machine learning model for the bot\. When you test the bot in the console, the console uses the runtime API to send user input back to Amazon Lex\. Amazon Lex then uses the machine learning model to interpret the user input\. 

1. The console shows the ScheduleAppointment bot\. On the **Editor** tab, review the preconfigured intent \(`MakeAppointment`\) details\.

1. Test the bot in the test window\. Use the following screen shot to engage in a test conversation with your bot:   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lex/latest/dg/images/appt-test-no-lambda.png)

   Note the following:
   + From the initial user input \("Book an appointment"\), the bot infers the intent \(`MakeAppointment`\)\. 
   + The bot then uses the configured prompts to get slot data from the user\. 
   + The bot blueprint has the `MakeAppointment` intent configured with the following confirmation prompt:

     ```
     {Time} is available, should I go ahead and book your appointment?
     ```

     After the user provides all of the slot data, Amazon Lex returns a response to the client with a confirmation prompt as the message\. The client displays the message for the user:

     ```
     16:00 is available, should I go ahead and book your appointment? 
     ```

   Notice that the bot accepts any appointment date and time values because you don't have any code to initialize or validate the user data\. In the next section, you add a Lambda function to do this\. 

**Next Step**  
[Step 2: Create a Lambda Function](ex1-sch-appt-create-lambda-function.md)