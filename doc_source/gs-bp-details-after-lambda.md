# Step 5 \(Optional\): Review the Details of the Information Flow \(Console\)<a name="gs-bp-details-after-lambda"></a>

This section explains the flow of information between the client and Amazon Lex for each user input, including the integration of the Lambda function\.

**Note**  
The section assumes that the client sends requests to Amazon Lex using the `PostText` runtime API and shows request and response details accordingly\. For an example of the information flow between the client and Amazon Lex in which client uses the `PostContent` API, see [Step 2a \(Optional\): Review the Details of the Spoken Information Flow \(Console\) ](gs-bp-details-postcontent-flow.md)\.

For more information about the `PostText` runtime API and additional details on the requests and responses shown in the following steps, see [PostText](API_runtime_PostText.md)\. 

1. User: I would like to order some flowers\.

   1. The client \(console\) sends the following [PostText](API_runtime_PostText.md) request to Amazon Lex: 

      ```
      POST /bot/OrderFlowers/alias/$LATEST/user/ignw84y6seypre4xly5rimopuri2xwnd/text
      "Content-Type":"application/json"
      "Content-Encoding":"amz-1.0"
      
      {
          "inputText": "I would like to order some flowers",
          "sessionAttributes": {}
      }
      ```

      Both the request URI and the body provide information to Amazon Lex:
      + Request URI – Provides bot name \(`OrderFlowers`\), bot alias \(`$LATEST`\), and user name \(a random string identifying the user\)\. The trailing `text` indicates that it is a `PostText` API request \(and not `PostContent`\)\.
      + Request body – Includes the user input \(`inputText`\) and empty `sessionAttributes`\. When the client makes the first request, there are no session attributes\. The Lambda function initiates them later\.

   1. From the `inputText`, Amazon Lex detects the intent \(`OrderFlowers`\)\. This intent is configured with a Lambda function as a code hook for user data initialization and validation\. Therefore, Amazon Lex invokes that Lambda function by passing the following information as event data:

      ```
      {
          "messageVersion": "1.0",
          "invocationSource": "DialogCodeHook",
          "userId": "ignw84y6seypre4xly5rimopuri2xwnd",
          "sessionAttributes": {},
          "bot": {
              "name": "OrderFlowers",
              "alias": null,
              "version": "$LATEST"
          },
          "outputDialogMode": "Text",
          "currentIntent": {
              "name": "OrderFlowers",
              "slots": {
                  "PickupTime": null,
                  "FlowerType": null,
                  "PickupDate": null
              },
              "confirmationStatus": "None"
          }
      }
      ```

      For more information, see [Input Event Format](lambda-input-response-format.md#using-lambda-input-event-format)\.

      In addition to the information that the client sent, Amazon Lex also includes the following additional data:
      + `messageVersion` – Currently Amazon Lex supports only the 1\.0 version\.
      + `invocationSource` – Indicates the purpose of Lambda function invocation\. In this case, it is to perform user data initialization and validation\. At this time, Amazon Lex knows that the user has not provided all the slot data to fulfill the intent\.
      + `currentIntent` information with all of the slot values set to null\.

   1. At this time, all the slot values are null\. There is nothing for the Lambda function to validate\. The Lambda function returns the following response to Amazon Lex:

      ```
      {
          "sessionAttributes": {},
          "dialogAction": {
              "type": "Delegate",
              "slots": {
                  "PickupTime": null,
                  "FlowerType": null,
                  "PickupDate": null
              }
          }
      }
      ```

      For information about the response format, see [Response Format](lambda-input-response-format.md#using-lambda-response-format)\.

      Note the following:
      + `dialogAction.type` – By setting this value to `Delegate`, Lambda function delegates the responsibility of deciding the next course of action to Amazon Lex\. 
**Note**  
If Lambda function detects anything in the user data validation, it instructs Amazon Lex what to do next, as shown in the next few steps\.

   1. According to the `dialogAction.type`, Amazon Lex decides the next course of action\. Because none of the slots are filled, it decides to elicit the value for the `FlowerType` slot\. It selects one of the value elicitation prompts \("What type of flowers would you like to order?"\) for this slot and sends the following response back to the client:  
![\[\]](http://docs.aws.amazon.com/lex/latest/dg/images/gs-1-details-10.png)

      The client displays the message in the response\.

1. User: roses

   1. The client sends the following [PostText](API_runtime_PostText.md) request to Amazon Lex: 

      ```
      POST /bot/OrderFlowers/alias/$LATEST/user/ignw84y6seypre4xly5rimopuri2xwnd/text
      "Content-Type":"application/json"
      "Content-Encoding":"amz-1.0"
      
      {
          "inputText": "roses",
          "sessionAttributes": {}
      }
      ```

      In the request body, the `inputText` provides user input\. The `sessionAttributes` remains empty\.

   1. Amazon Lex first interprets the `inputText` in the context of the current intent\. The service remembers that it had asked the specific user for information about the `FlowerType` slot\. It updates the slot value in the current intent and invokes the Lambda function with the following event data:

      ```
      {
          "messageVersion": "1.0",
          "invocationSource": "DialogCodeHook",
          "userId": "ignw84y6seypre4xly5rimopuri2xwnd",
          "sessionAttributes": {},
          "bot": {
              "name": "OrderFlowers",
              "alias": null,
              "version": "$LATEST"
          },
          "outputDialogMode": "Text",
          "currentIntent": {
              "name": "OrderFlowers",
              "slots": {
                  "PickupTime": null,
                  "FlowerType": "roses",
                  "PickupDate": null
              },
              "confirmationStatus": "None"
          }
      }
      ```

      Note the following:
      + `invocationSource` – continues to be `DialogCodeHook` \(we are simply validating user data\)\. 
      + `currentIntent.slots` – Amazon Lex has updated the `FlowerType` slot to roses\.

   1. According to the `invocationSource` value of `DialogCodeHook`, the Lambda function performs user data validation\. It recognizes `roses` as a valid slot value \(and sets `Price` as a session attribute\) and returns the following response to Amazon Lex\. 

      ```
      {
          "sessionAttributes": {
              "Price": 25
          },
          "dialogAction": {
              "type": "Delegate",
              "slots": {
                  "PickupTime": null,
                  "FlowerType": "roses",
                  "PickupDate": null
              }
          }
      }
      ```

      Note the following:
      + `sessionAttributes` – Lambda function has added `Price` \(of the roses\) as a session attribute\.
      + `dialogAction.type` – is set to `Delegate`\. The user data was valid so the Lambda function directs Amazon Lex to choose the next course of action\.

       

   1. According to the `dialogAction.type`, Amazon Lex chooses the next course of action\. Amazon Lex knows it needs more slot data so it picks the next unfilled slot \(`PickupDate`\) with the highest priority according to the intent configuration\. Amazon Lex selects one of the value\-elicitation prompt messages—"What day do you want the roses to be picked up?"—for this slot according to the intent configuration, and then sends the following response back to the client:   
![\[\]](http://docs.aws.amazon.com/lex/latest/dg/images/gs-1-details-20.png)

      The client simply displays the message in the response – "What day do you want the roses to be picked up?\."

1. User: tomorrow

   1. The client sends the following [PostText](API_runtime_PostText.md) request to Amazon Lex: 

      ```
      POST /bot/OrderFlowers/alias/$LATEST/user/ignw84y6seypre4xly5rimopuri2xwnd/text
      "Content-Type":"application/json"
      "Content-Encoding":"amz-1.0"
      
      {
          "inputText": "tomorrow",
          "sessionAttributes": {
              "Price": "25"
          }
      }
      ```

      In the request body, `inputText` provides user input and the client passes the session attributes back to the service\.

   1. Amazon Lex remembers the context—that it was eliciting data for the `PickupDate` slot\. In this context, it knows the `inputText` value is for the `PickupDate` slot\. Amazon Lex then invokes the Lambda function by sending the following event: 

      ```
      {
          "messageVersion": "1.0",
          "invocationSource": "DialogCodeHook",
          "userId": "ignw84y6seypre4xly5rimopuri2xwnd",
          "sessionAttributes": {
              "Price": "25"
          },
          "bot": {
              "name": "OrderFlowersCustomWithRespCard",
              "alias": null,
              "version": "$LATEST"
          },
          "outputDialogMode": "Text",
          "currentIntent": {
              "name": "OrderFlowers",
              "slots": {
                  "PickupTime": null,
                  "FlowerType": "roses",
                  "PickupDate": "2017-01-05"
              },
              "confirmationStatus": "None"
          }
      }
      ```

      Amazon Lex has updated the `currentIntent.slots` by setting the `PickupDate` value\. Also note that the service passes the `sessionAttributes` as it is to the Lambda function\.

   1. As per `invocationSource` value of `DialogCodeHook`, the Lambda function performs user data validation\. It recognizes `PickupDate` slot value is valid and returns the following response to Amazon Lex: 

      ```
      {
          "sessionAttributes": {
              "Price": 25
          },
          "dialogAction": {
              "type": "Delegate",
              "slots": {
                  "PickupTime": null,
                  "FlowerType": "roses",
                  "PickupDate": "2017-01-05"
              }
          }
      }
      ```

      Note the following:
      + `sessionAttributes` – No change\.
      + `dialogAction.type` – is set to `Delegate`\. The user data was valid, and the Lambda function directs Amazon Lex to choose the next course of action\.

   1. According to the `dialogAction.type`, Amazon Lex chooses the next course of action\. Amazon Lex knows it needs more slot data so it picks the next unfilled slot \(`PickupTime`\) with the highest priority according to the intent configuration\. Amazon Lex selects one of the prompt messages \("Deliver the roses at what time on 2017\-01\-05?"\) for this slot according to the intent configuration and sends the following response back to the client:   
![\[\]](http://docs.aws.amazon.com/lex/latest/dg/images/gs-1-details-30.png)

      The client displays the message in the response – "Deliver the roses at what time on 2017\-01\-05?"

1. User: 4 pm

   1. The client sends the following [PostText](API_runtime_PostText.md) request to Amazon Lex: 

      ```
      POST /bot/OrderFlowers/alias/$LATEST/user/ignw84y6seypre4xly5rimopuri2xwnd/text
      "Content-Type":"application/json"
      "Content-Encoding":"amz-1.0"
      
      {
          "inputText": "4 pm",
          "sessionAttributes": {
              "Price": "25"
          }
      }
      ```

      In the request body, `inputText` provides user input\. The client passes the `sessionAttributes` in the request\.

   1. Amazon Lex understands context\. It understands that it was eliciting data for the `PickupTime` slot\. In this context, it knows that the `inputText` value is for the `PickupTime` slot\. Amazon Lex then invokes the Lambda function by sending the following event: 

      ```
      {
          "messageVersion": "1.0",
          "invocationSource": "DialogCodeHook",
          "userId": "ignw84y6seypre4xly5rimopuri2xwnd",
          "sessionAttributes": {
              "Price": "25"
          },
          "bot": {
              "name": "OrderFlowersCustomWithRespCard",
              "alias": null,
              "version": "$LATEST"
          },
          "outputDialogMode": "Text",
          "currentIntent": {
              "name": "OrderFlowers",
              "slots": {
                  "PickupTime": "16:00",
                  "FlowerType": "roses",
                  "PickupDate": "2017-01-05"
              },
              "confirmationStatus": "None"
          }
      }
      ```

      Amazon Lex has updated the `currentIntent.slots` by setting the `PickupTime` value\.

   1. According to the `invocationSource` value of `DialogCodeHook`, the Lambda function performs user data validation\. It recognizes `PickupDate` slot value is valid and returns the following response to Amazon Lex\. 

      ```
      {
          "sessionAttributes": {
              "Price": 25
          },
          "dialogAction": {
              "type": "Delegate",
              "slots": {
                  "PickupTime": "16:00",
                  "FlowerType": "roses",
                  "PickupDate": "2017-01-05"
              }
          }
      }
      ```

      Note the following:
      + `sessionAttributes` – No change in session attribute\.
      + `dialogAction.type` – is set to `Delegate`\. The user data was valid so the Lambda function directs Amazon Lex to choose the next course of action\.

   1. At this time Amazon Lex knows it has all the slot data\. This intent is configured with a confirmation prompt\. Therefore, Amazon Lex sends the following response to the user asking for confirmation before fulfilling the intent:   
![\[\]](http://docs.aws.amazon.com/lex/latest/dg/images/gs-1-details-45.png)

      The client simply displays the message in the response and waits for the user response\.

1. User: Yes

   1. The client sends the following [PostText](API_runtime_PostText.md) request to Amazon Lex: 

      ```
      POST /bot/OrderFlowers/alias/$LATEST/user/ignw84y6seypre4xly5rimopuri2xwnd/text
      "Content-Type":"application/json"
      "Content-Encoding":"amz-1.0"
      
      {
          "inputText": "yes",
          "sessionAttributes": {
              "Price": "25"
          }
      }
      ```

   1. Amazon Lex interprets the `inputText` in the context of confirming the current intent\. Amazon Lex understands that the user wants to proceed with the order\. This time Amazon Lex invokes the Lambda function to fulfill the intent by sending the following event, which sets the `invocationSource` to `FulfillmentCodeHook` in the event it sends to the Lambda function\. Amazon Lex also sets the `confirmationStatus` to `Confirmed`\.

      ```
      {
          "messageVersion": "1.0",
          "invocationSource": "FulfillmentCodeHook",
          "userId": "ignw84y6seypre4xly5rimopuri2xwnd",
          "sessionAttributes": {
              "Price": "25"
          },
          "bot": {
              "name": "OrderFlowersCustomWithRespCard",
              "alias": null,
              "version": "$LATEST"
          },
          "outputDialogMode": "Text",
          "currentIntent": {
              "name": "OrderFlowers",
              "slots": {
                  "PickupTime": "16:00",
                  "FlowerType": "roses",
                  "PickupDate": "2017-01-05"
              },
              "confirmationStatus": "Confirmed"
          }
      }
      ```

      Note the following:
      + `invocationSource` – This time Amazon Lex set this value to `FulfillmentCodeHook`, directing the Lambda function to fulfill the intent\.
      + `confirmationStatus` – is set to `Confirmed`\.

   1. This time, the Lambda function fulfills the `OrderFlowers` intent, and returns the following response:

      ```
      {
          "sessionAttributes": {
              "Price": "25"
          },
          "dialogAction": {
              "type": "Close",
              "fulfillmentState": "Fulfilled",
              "message": {
                  "contentType": "PlainText",
                  "content": "Thanks, your order for roses has been placed and will be ready for pickup by 16:00 on 2017-01-05"
              }
          }
      }
      ```

      Note the following: 
      + Sets the `dialogAction.type` – The Lambda function sets this value to `Close`, directing Amazon Lex to not expect a user response\. 
      + `dialogAction.fulfillmentState` – is set to Fulfilled and includes an appropriate `message` to convey to the user\.

   1. Amazon Lex reviews the `fulfillmentState` and sends the following response back to the client\. 

      Amazon Lex then returns the following to the client:  
![\[\]](http://docs.aws.amazon.com/lex/latest/dg/images/gs-1-details-48.png)

      Note that:
      + `dialogState` – Amazon Lex sets this value to `fulfilled`\.
      + `message` – is the same message that the Lambda function provided\.

      The client displays the message\.

1. Now test the bot again\. To establish a new \(user\) context, choose the **Clear** link in the test window\. Now provide invalid slot data for the `OrderFlowers` intent\. This time the Lambda function performs the data validation, resets invalid slot data value to null, and asks Amazon Lex to prompt the user for valid data\. For example, try the following:
   + Jasmine as the flower type \(it is not one of the supported flower types\)\.
   + Yesterday as the day when you want to pick up the flowers\.
   + After placing your order, enter another flower type instead of replying "yes" to confirm the order\. In response, the Lambda function updates the `Price` in the session attribute, keeping a running total of flower orders\.

   The Lambda function also performs the fulfillment activity\. 

**Next Step**  
[Step 6: Update the Intent Configuration to Add an Utterance \(Console\)](gs-bp-utterance.md)