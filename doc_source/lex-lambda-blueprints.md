# Amazon Lex and AWS Lambda Blueprints<a name="lex-lambda-blueprints"></a>

The Amazon Lex console provides example bots \(called bot blueprints\) that are preconfigured so you can quickly create and test a bot in the console\. For each of these bot blueprints, Lambda function blueprints are also provided\. These blueprints provide sample code that works with their corresponding bots\. You can use these blueprints to quickly create a bot that is configured with a Lambda function as a code hook, and test the end\-to\-end setup without having to write code\.

You can use the following Amazon Lex bot blueprints and the corresponding AWS Lambda function blueprints as code hooks for bots: 
+ Amazon Lex blueprint — `OrderFlowers`
  + AWS Lambda blueprint — `lex-order-flowers-python`
+ Amazon Lex blueprint — `ScheduleAppointment` 
  + AWS Lambda blueprint — `lex-make-appointment-python`
+ Amazon Lex blueprint — `BookTrip`
  + AWS Lambda blueprint — `lex-book-trip-python`

To create a bot using a blueprint and configure it to use a Lambda function as a code hook, see [Exercise 1: Create an Amazon Lex Bot Using a Blueprint \(Console\)](gs-bp.md)\. For an example of using other blueprints, see [Additional Examples: Creating Amazon Lex Bots](additional-exercises.md)\.

## Updating a Blueprint for a Specific Locale<a name="blueprint-update-locale"></a>

If you are using a blueprint in a locale other than English \(US\) \(en\-US\), you need to update the name of any intents to include the locale\. For example, if you are using the `OrderFlowers` blueprint, you need to do the following\.
+ Find the `dispatch` function near the end of the Lambda function code\.
+ In the `dispatch` function, update the name of the intent to include the locale that you are using\. For example, if you are using the English \(Australian\) \(en\-AU\) locale, change the line:

  `if intent_name == 'OrderFlowers':`

  to

  `if intent_name == 'OrderFlowers_enAU':`

Other blueprints use other intent names, they should be updated as above before you use them\.