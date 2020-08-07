# Step 1: Create a Lambda Function<a name="gs2-prepare"></a>

First, create a Lambda function which fulfills a pizza order\. You specify this function in your Amazon Lex bot, which you create in the next section\.

**To create a Lambda function**

1. Sign in to the AWS Management Console and open the AWS Lambda console at [https://console\.aws\.amazon\.com/lambda/](https://console.aws.amazon.com/lambda/)\.

1. Choose **Create function**\.

1. On the **Create function** page, choose **Author from scratch**\. 

   Because you are using custom code provided to you in this exercise to create a Lambda function, you choose author the function from scratch\.

   Do the following:

   1. Type the name \(`PizzaOrderProcessor`\)\.

   1. For the **Runtime**, choose the latest version of Node\.js\.

   1. For the **Role**, choose **Create new role from template\(s\)**\.

   1. Enter a new role name \(`PizzaOrderProcessorRole`\)\.

   1. Choose **Create function**\.

1. On the function page, do the following: 

   In the **Function code** section, choose **Edit code inline**, and then copy the following Node\.js function code and paste it in the window\. 

   ```
   'use strict';
        
   // Close dialog with the customer, reporting fulfillmentState of Failed or Fulfilled ("Thanks, your pizza will arrive in 20 minutes")
   function close(sessionAttributes, fulfillmentState, message) {
       return {
           sessionAttributes,
           dialogAction: {
               type: 'Close',
               fulfillmentState,
               message,
           },
       };
   }
    
   // --------------- Events -----------------------
    
   function dispatch(intentRequest, callback) {
       console.log(`request received for userId=${intentRequest.userId}, intentName=${intentRequest.currentIntent.name}`);
       const sessionAttributes = intentRequest.sessionAttributes;
       const slots = intentRequest.currentIntent.slots;
       const crust = slots.crust;
       const size = slots.size;
       const pizzaKind = slots.pizzaKind;
       
       callback(close(sessionAttributes, 'Fulfilled',
       {'contentType': 'PlainText', 'content': `Okay, I have ordered your ${size} ${pizzaKind} pizza on ${crust} crust`}));
       
   }
    
   // --------------- Main handler -----------------------
    
   // Route the incoming request based on intent.
   // The JSON body of the request is provided in the event slot.
   exports.handler = (event, context, callback) => {
       try {
           dispatch(event,
               (response) => {
                   callback(null, response);
               });
       } catch (err) {
           callback(err);
       }
   };
   ```

1. Choose **Save**\.

## Test the Lambda Function Using Sample Event Data<a name="gs2-lambdafunction-test"></a>

In the console, test the Lambda function by using sample event data to manually invoke it\. 

**To test the Lambda function:**

1. Sign in to the AWS Management Console and open the AWS Lambda console at [https://console\.aws\.amazon\.com/lambda/](https://console.aws.amazon.com/lambda/)\.

1. On the **Lambda function** page, choose the Lambda function \(`PizzaOrderProcessor).`

1. On the function page, in the list of test events, choose **Configure test events**\.

1. On the **Configure test event** page, do the following: 

   1. Choose **Create new test event**\.

   1. In the **Event name** field, enter a name for the event \(`PizzaOrderProcessorTest`\)\.

   1. Copy the following Amazon Lex event into the window\. 

      ```
      {
        "messageVersion": "1.0",
        "invocationSource": "FulfillmentCodeHook",
        "userId": "user-1",
        "sessionAttributes": {},
        "bot": {
          "name": "PizzaOrderingApp",
          "alias": "$LATEST",
          "version": "$LATEST"
        },
        "outputDialogMode": "Text",
        "currentIntent": {
          "name": "OrderPizza",
          "slots": {
            "size": "large",
            "pizzaKind": "meat",
            "crust": "thin"
          },
          "confirmationStatus": "None"
        }
      }
      ```

1. Choose **Create**\.

AWS Lambda creates the test and you go back to the function page\. Choose **Test** and Lambda runs your Lambda function\.

In the result box, choose **Details**\. The console displays the following output in the **Execution result** pane\. 

```
{
  "sessionAttributes": {},
  "dialogAction": {
    "type": "Close",
    "fulfillmentState": "Fulfilled",
    "message": {
      "contentType": "PlainText",
      "content": "Okay, I have ordered your large meat pizza on thin crust."
    }
}
```

## Next Step<a name="gs2-next-step-create-bot"></a>

[Step 2: Create a Bot](gs2-create-bot.md)