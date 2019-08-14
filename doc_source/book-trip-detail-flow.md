# Details of the Information Flow<a name="book-trip-detail-flow"></a>

In this exercise, you engaged in a conversation with the Amazon Lex BookTrip bot using the test window client provided in the Amazon Lex console\. This section explains the following: 
+ The data flow between the client and Amazon Lex\.

   

  The section assumes that the client sends requests to Amazon Lex using the `PostText` runtime API and shows request and response details accordingly\. For more information about the `PostText` runtime API, see [PostText](API_runtime_PostText.md)\.
**Note**  
For an example of the information flow between the client and Amazon Lex in which the client uses the `PostContent` API, see [Step 2a \(Optional\): Review the Details of the Spoken Information Flow \(Console\) ](gs-bp-details-postcontent-flow.md)\.

   
+ The data flow between Amazon Lex and the Lambda function\. For more information, see [Lambda Function Input Event and Response Format](lambda-input-response-format.md)\.

**Topics**
+ [Data Flow: Book Hotel Intent](#data-flow-book-hotel)
+ [Data Flow: Book Car Intent](#data-flow-book-car)

## Data Flow: Book Hotel Intent<a name="data-flow-book-hotel"></a>

This section explains what happens after each user input\.

1. User: "book a hotel"

   1. The client \(console\) sends the following [PostText](API_runtime_PostText.md) request to Amazon Lex:

      ```
      POST /bot/BookTrip/alias/$LATEST/user/wch89kjqcpkds8seny7dly5x3otq68j3/text
      "Content-Type":"application/json"
      "Content-Encoding":"amz-1.0"
      
      {
         "inputText":"book a hotel",
         "sessionAttributes":{}
      }
      ```

      Both the request URI and the body provides information to Amazon Lex:
      + Request URI – Provides bot name \(BookTrip\), bot alias \($LATEST\) and the user name\. The trailing `text` indicates that it is a `PostText` API request \(and not `PostContent`\)\.
      + Request body – Includes the user input \(`inputText`\) and empty `sessionAttributes`\. Initially, this is an empty object and the Lambda function first sets the session attributes\.

   1. From the `inputText`, Amazon Lex detects the intent \(BookHotel\)\. This intent is configured with a Lambda function as a code hook for user data initialization/validation\. Therefore, Amazon Lex invokes that Lambda function by passing the following information as the event parameter \(see [Input Event Format](lambda-input-response-format.md#using-lambda-input-event-format)\):

      ```
      {
         "messageVersion":"1.0",
         "invocationSource":"DialogCodeHook",
         "userId":"wch89kjqcpkds8seny7dly5x3otq68j3",
         "sessionAttributes":{
         },
         "bot":{
            "name":"BookTrip",
            "alias":null,
            "version":"$LATEST"
         },
         "outputDialogMode":"Text",
         "currentIntent":{
            "name":"BookHotel",
            "slots":{
               "RoomType":null,
               "CheckInDate":null,
               "Nights":null,
               "Location":null
            },
            "confirmationStatus":"None"
         }
      }
      ```

      In addition to the information sent by the client, Amazon Lex also includes the following additional data:
      + `messageVersion` – Currently Amazon Lex supports only the 1\.0 version\.
      + `invocationSource` – Indicates the purpose of Lambda function invocation\. In this case, it is to perform user data initialization and validation \(at this time Amazon Lex knows that the user has not provided all the slot data to fulfill the intent\)\.
      + `currentIntent` – All of the slot values are set to null\.

   1. At this time, all the slot values are null\. There is nothing for the Lambda function to validate\. The Lambda function returns the following response to Amazon Lex\. For information about response format, see [Response Format](lambda-input-response-format.md#using-lambda-response-format)\. 

      ```
      {
         "sessionAttributes":{
            "currentReservation":"{\"ReservationType\":\"Hotel\",\"Location\":null,\"RoomType\":null,\"CheckInDate\":null,\"Nights\":null}"
         },
         "dialogAction":{
            "type":"Delegate",
            "slots":{
               "RoomType":null,
               "CheckInDate":null,
               "Nights":null,
               "Location":null
            }
         }
      }
      ```
**Note**  
`currentReservation` – The Lambda function includes this session attribute\. Its value is a copy of the current slot information and the reservation type\.   
Only the Lambda function and the client can update these session attributes\. Amazon Lex simply passes these values\.
`dialogAction.type` – By setting this value to `Delegate`, the Lambda function delegates the responsibility for the next course of action to Amazon Lex\.   
If the Lambda function detected anything in the user data validation, it instructs Amazon Lex what to do next\.

   1. As per the `dialogAction.type`, Amazon Lex decides the next course of action—elicit data from the user for the `Location` slot\. It selects one of the prompt messages \("What city will you be staying in?"\) for this slot, according to the intent configuration, and then sends the following response to the user:   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lex/latest/dg/images/book-hotel-10.png)

      The session attributes are passed to the client\.

      The client reads the response and then displays the message: "What city will you be staying in?"

1. User: "Moscow"

   1. The client sends the following `PostText` request to Amazon Lex \(line breaks added for readability\):

      ```
      POST /bot/BookTrip/alias/$LATEST/user/wch89kjqcpkds8seny7dly5x3otq68j3/text
      "Content-Type":"application/json"
      "Content-Encoding":"amz-1.0"
      
      {
         "inputText":"Moscow",
         "sessionAttributes":{
             "currentReservation":"{\"ReservationType\":\"Hotel\",
                                    \"Location\":null,
                                    \"RoomType\":null,
                                    \"CheckInDate\":null,
                                    \"Nights\":null}"
         }
      }
      ```

      In addition to the `inputText`, the client includes the same `currentReservation` session attributes it received\. 

   1. Amazon Lex first interprets the `inputText` in the context of the current intent \(the service remembers that it had asked the specific user for information about `Location` slot\)\. It updates the slot value for the current intent and invokes the Lambda function using the following event:

      ```
      {
          "messageVersion": "1.0",
          "invocationSource": "DialogCodeHook",
          "userId": "wch89kjqcpkds8seny7dly5x3otq68j3",
          "sessionAttributes": {
              "currentReservation": "{\"ReservationType\":\"Hotel\",\"Location\":null,\"RoomType\":null,\"CheckInDate\":null,\"Nights\":null}"
          },
          "bot": {
              "name": "BookTrip",
              "alias": null,
              "version": "$LATEST"
          },
          "outputDialogMode": "Text",
          "currentIntent": {
              "name": "BookHotel",
              "slots": {
                  "RoomType": null,
                  "CheckInDate": null,
                  "Nights": null,
                  "Location": "Moscow"
              },
              "confirmationStatus": "None"
          }
      }
      ```
**Note**  
`invocationSource` continues to be `DialogCodeHook`\. In this step, we are just validating user data\.
Amazon Lex is just passing the session attribute to the Lambda function\.
For `currentIntent.slots`, Amazon Lex has updated the `Location` slot to `Moscow`\.

   1. The Lambda function performs the user data validation and determines that `Moscow` is an invalid location\. 
**Note**  
The Lambda function in this exercise has a simple list of valid cities and `Moscow` is not on the list\. In a production application, you might use a back\-end database to get this information\. 

      It resets the slot value back to null and directs Amazon Lex to prompt the user again for another value by sending the following response:

      ```
      {
          "sessionAttributes": {
              "currentReservation": "{\"ReservationType\":\"Hotel\",\"Location\":\"Moscow\",\"RoomType\":null,\"CheckInDate\":null,\"Nights\":null}"
          },
          "dialogAction": {
              "type": "ElicitSlot",
              "intentName": "BookHotel",
              "slots": {
                  "RoomType": null,
                  "CheckInDate": null,
                  "Nights": null,
                  "Location": null
              },
              "slotToElicit": "Location",
              "message": {
                  "contentType": "PlainText",
                  "content": "We currently do not support Moscow as a valid destination.  Can you try a different city?"
              }
          }
      }
      ```
**Note**  
`currentIntent.slots.Location` is reset to null\.
`dialogAction.type` is set to `ElicitSlot`, which directs Amazon Lex to prompt the user again by providing the following:   
`dialogAction.slotToElicit` – slot for which to elicit data from the user\.
`dialogAction.message` – a `message` to convey to the user\.

   1. Amazon Lex notices the `dialogAction.type` and passes the information to the client in the following response:  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lex/latest/dg/images/book-hotel-20.png)

      The client simply displays the message: "We currently do not support Moscow as a valid destination\. Can you try a different city?"

1. User: "Chicago"

   1. The client sends the following `PostText` request to Amazon Lex:

      ```
      POST /bot/BookTrip/alias/$LATEST/user/wch89kjqcpkds8seny7dly5x3otq68j3/text
      "Content-Type":"application/json"
      "Content-Encoding":"amz-1.0"
      
      {
         "inputText":"Chicago",
         "sessionAttributes":{
             "currentReservation":"{\"ReservationType\":\"Hotel\",
                                    \"Location\":\"Moscow\",
                                    \"RoomType\":null,
                                    \"CheckInDate\":null,
                                    \"Nights\":null}"
         }
      }
      ```

   1. Amazon Lex knows the context, that it was eliciting data for the `Location` slot\. In this context, it knows the `inputText` value is for the `Location` slot\. It then invokes the Lambda function by sending the following event: 

      ```
      {
          "messageVersion": "1.0",
          "invocationSource": "DialogCodeHook",
          "userId": "wch89kjqcpkds8seny7dly5x3otq68j3",
          "sessionAttributes": {
              "currentReservation": "{\"ReservationType\":\"Hotel\",\"Location\":Moscow,\"RoomType\":null,\"CheckInDate\":null,\"Nights\":null}"
          },
          "bot": {
              "name": "BookTrip",
              "alias": null,
              "version": "$LATEST"
          },
          "outputDialogMode": "Text",
          "currentIntent": {
              "name": "BookHotel",
              "slots": {
                  "RoomType": null,
                  "CheckInDate": null,
                  "Nights": null,
                  "Location": "Chicago"
              },
              "confirmationStatus": "None"
          }
      }
      ```

      Amazon Lex updated the `currentIntent.slots` by setting the `Location` slot to `Chicago`\. 

   1. According to the `invocationSource` value of `DialogCodeHook`, the Lambda function performs user data validation\. It recognizes `Chicago` as a valid slot value, updates the session attribute accordingly, and then returns the following response to Amazon Lex\. 

      ```
      {
          "sessionAttributes": {
              "currentReservation": "{\"ReservationType\":\"Hotel\",\"Location\":\"Chicago\",\"RoomType\":null,\"CheckInDate\":null,\"Nights\":null}"
          },
          "dialogAction": {
              "type": "Delegate",
              "slots": {
                  "RoomType": null,
                  "CheckInDate": null,
                  "Nights": null,
                  "Location": "Chicago"
              }
          }
      }
      ```
**Note**  
`currentReservation` – The Lambda function updates this session attribute by setting the `Location` to `Chicago`\. 
`dialogAction.type` – Is set to `Delegate`\. User data was valid, and the Lambda function directs Amazon Lex to choose the next course of action\.

       

   1. According to `dialogAction.type`, Amazon Lex chooses the next course of action\. Amazon Lex knows that it needs more slot data and picks the next unfilled slot \(`CheckInDate`\) with the highest priority according to the intent configuration\. It selects one of the prompt messages \("What day do you want to check in?"\) for this slot according to the intent configuration and then sends the following response back to the client:   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lex/latest/dg/images/book-hotel-30.png)

      The client displays the message: "What day do you want to check in?" 

1. The user interaction continues—the user provides data, the Lambda function validates data, and then delegates the next course of action to Amazon Lex\. Eventually the user provides all of the slot data, the Lambda function validates all of the user input, and then Amazon Lex recognizes it has all the slot data\. 
**Note**  
In this exercise, after the user provides all of the slot data, the Lambda function computes the price of the hotel reservation and returns it as another session attribute \(`currentReservationPrice`\)\. 

   At this point, the intent is ready to be fulfilled, but the BookHotel intent is configured with a confirmation prompt requiring user confirmation before Amazon Lex can fulfill the intent\. Therefore, Amazon Lex sends the following message to the client requesting confirmation before booking the hotel:  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lex/latest/dg/images/book-hotel-40.png)

   The client display the message: "Okay, I have you down for a 5 night in Chicago starting 2016\-12\-18\. Shall I book the reservation?"

1. User: "yes"

   1. The client sends the following `PostText` request to Amazon Lex: 

      ```
      POST /bot/BookTrip/alias/$LATEST/user/wch89kjqcpkds8seny7dly5x3otq68j3/text
      "Content-Type":"application/json"
      "Content-Encoding":"amz-1.0"
      
      {
         "inputText":"Yes",
         "sessionAttributes":{
             "currentReservation":"{\"ReservationType\":\"Hotel\",
                                    \"Location\":\"Chicago\",
                                    \"RoomType\":\"queen\",
                                    \"CheckInDate\":\"2016-12-18\",
                                    \"Nights\":\"5\"}",
            "currentReservationPrice":"1195"
         }
      }
      ```

   1. Amazon Lex interprets the `inputText` in the context of confirming the current intent\. Amazon Lex understands that the user wants to proceed with the reservation\. This time Amazon Lex invokes the Lambda function to fulfill the intent by sending the following event\. By setting the `invocationSource` to `FulfillmentCodeHook` in the event, it sends to the Lambda function\. Amazon Lex also sets the `confirmationStatus` to `Confirmed`\.

      ```
      {
          "messageVersion": "1.0",
          "invocationSource": "FulfillmentCodeHook",
          "userId": "wch89kjqcpkds8seny7dly5x3otq68j3",
          "sessionAttributes": {
              "currentReservation": "{\"ReservationType\":\"Hotel\",\"Location\":\"Chicago\",\"RoomType\":\"queen\",\"CheckInDate\":\"2016-12-18\",\"Nights\":\"5\"}",
              "currentReservationPrice": "956"
          },
          "bot": {
              "name": "BookTrip",
              "alias": null,
              "version": "$LATEST"
          },
          "outputDialogMode": "Text",
          "currentIntent": {
              "name": "BookHotel",
              "slots": {
                  "RoomType": "queen",
                  "CheckInDate": "2016-12-18",
                  "Nights": "5",
                  "Location": "Chicago"
              },
              "confirmationStatus": "Confirmed"
          }
      }
      ```
**Note**  
`invocationSource` – This time, Amazon Lex set this value to `FulfillmentCodeHook`, directing the Lambda function to fulfill the intent\.
`confirmationStatus` – Is set to `Confirmed`\.

   1. This time, the Lambda function fulfills the BookHotel intent, Amazon Lex completes the reservation, and then it returns the following response: 

      ```
      {
          "sessionAttributes": {
              "lastConfirmedReservation": "{\"ReservationType\":\"Hotel\",\"Location\":\"Chicago\",\"RoomType\":\"queen\",\"CheckInDate\":\"2016-12-18\",\"Nights\":\"5\"}"
          },
          "dialogAction": {
              "type": "Close",
              "fulfillmentState": "Fulfilled",
              "message": {
                  "contentType": "PlainText",
                  "content": "Thanks, I have placed your reservation.   Please let me know if you would like to book a car rental, or another hotel."
              }
          }
      }
      ```
**Note**  
 `lastConfirmedReservation` – Is a new session attribute that the Lambda function added \(instead of the `currentReservation`, `currentReservationPrice`\)\. 
`dialogAction.type` – The Lambda function sets this value to `Close`, indicating that Amazon Lex to not expect a user response\. 
`dialogAction.fulfillmentState` – Is set to `Fulfilled` and includes an appropriate `message` to convey to the user\.

   1. Amazon Lex reviews the `fulfillmentState` and sends the following response to the client:  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lex/latest/dg/images/book-hotel-60.png)
**Note**  
`dialogState` – Amazon Lex sets this value to `Fulfilled`\.
`message` – Is the same message that the Lambda function provided\.

       The client displays the message\.

## Data Flow: Book Car Intent<a name="data-flow-book-car"></a>

The BookTrip bot in this exercise supports two intents \(BookHotel and BookCar\)\. After booking a hotel, the user can continue the conversation to book a car\. As long as the session hasn't timed out, in each subsequent request the client continues to send the session attributes \(in this example, the `lastConfirmedReservation`\)\. The Lambda function can use this information to initialize slot data for the BookCar intent\. This shows how you can use session attributes in cross\-intent data sharing\. 

Specifically, when the user chooses the BookCar intent, the Lambda function uses relevant information in the session attribute to prepopulate slots \(PickUpDate, ReturnDate, and PickUpCity\) for the BookCar intent\.

**Note**  
The Amazon Lex console provides the **Clear** link that you can use to clear any prior session attributes\. 

Follow the steps in this procedure to continue the conversation\.

1. User: "also book a car"

   1. The client sends the following `PostText` request to Amazon Lex\.

      ```
      POST /bot/BookTrip/alias/$LATEST/user/wch89kjqcpkds8seny7dly5x3otq68j3/text
      "Content-Type":"application/json"
      "Content-Encoding":"amz-1.0"
      
      {
         "inputText":"also book a car",
         "sessionAttributes":{
             "lastConfirmedReservation":""{\"ReservationType\":\"Hotel\",
                                           \"Location\":\"Chicago\",
                                           \"RoomType\":\"queen\",
                                           \"CheckInDate\":\"2016-12-18\",
                                           \"Nights\":\"5\"}"
         }
      }
      ```

      The client includes the `lastConfirmedReservation` session attribute\.

   1. Amazon Lex detects the intent \(BookCar\) from the `inputText`\. This intent is also configured to invoke the Lambda function to perform the initialization and validation of the user data\. Amazon Lex invokes the Lambda function with the following event:

      ```
      {
          "messageVersion": "1.0",
          "invocationSource": "DialogCodeHook",
          "userId": "wch89kjqcpkds8seny7dly5x3otq68j3",
          "sessionAttributes": {
              "lastConfirmedReservation": "{\"ReservationType\":\"Hotel\",\"Location\":\"Chicago\",\"RoomType\":\"queen\",\"CheckInDate\":\"2016-12-18\",\"Nights\":\"5\"}"
          },
          "bot": {
              "name": "BookTrip",
              "alias": null,
              "version": "$LATEST"
          },
          "outputDialogMode": "Text",
          "currentIntent": {
              "name": "BookCar",
              "slots": {
                  "PickUpDate": null,
                  "ReturnDate": null,
                  "DriverAge": null,
                  "CarType": null,
                  "PickUpCity": null
              },
              "confirmationStatus": "None"
          }
      }
      ```
**Note**  
 `messageVersion` – Currently Amazon Lex supports the 1\.0 version only\.
`invocationSource` – Indicates the purpose of invocation is to perform initialization and user data validation\.
`currentIntent` – It includes the intent name and the slots\. At this time, all slot values are null\.

   1. The Lambda function notices all null slot values with nothing to validate\. However, it uses session attributes to initialize some of the slot values \(`PickUpDate`, `ReturnDate`, and `PickUpCity`\), and then returns the following response:

      ```
      {
          "sessionAttributes": {
              "lastConfirmedReservation": "{\"ReservationType\":\"Hotel\",\"Location\":\"Chicago\",\"RoomType\":\"queen\",\"CheckInDate\":\"2016-12-18\",\"Nights\":\"5\"}",
              "currentReservation": "{\"ReservationType\":\"Car\",\"PickUpCity\":null,\"PickUpDate\":null,\"ReturnDate\":null,\"CarType\":null}",
              "confirmationContext": "AutoPopulate"
          },
          "dialogAction": {
              "type": "ConfirmIntent",
              "intentName": "BookCar",
              "slots": {
                  "PickUpCity": "Chicago",
                  "PickUpDate": "2016-12-18",
                  "ReturnDate": "2016-12-22",
                  "CarType": null,
                  "DriverAge": null
              },
              "message": {
                  "contentType": "PlainText",
                  "content": "Is this car rental for your 5 night stay in Chicago on 2016-12-18?"
              }
          }
      }
      ```
**Note**  
In addition to the `lastConfirmedReservation`, the Lambda function includes more session attributes \(`currentReservation` and `confirmationContext`\)\. 
`dialogAction.type` is set to `ConfirmIntent`, which informs Amazon Lex that a yes, no reply is expected from the user \(the confirmationContext set to AutoPopulate, the Lambda function knows that the yes/no user reply is to obtain user confirmation of the initialization the Lambda function performed \(auto populated slot data\)\.   
   
The Lambda function also includes in the response an informative message in the `dialogAction.message` for Amazon Lex to return to the client\.  
The term `ConfirmIntent` \(value of the `dialogAction.type`\) is not related to any bot intent\. In the example, Lambda function uses this term to direct Amazon Lex to get a yes/no reply from the user\.

   1. According to the `dialogAction.type`, Amazon Lex returns the following response to the client:   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lex/latest/dg/images/book-car-10.png)

      The client displays the message: "Is this car rental for your 5 night stay in Chicago on 2016\-12\-18?"

1. User: "yes"

   1. The client sends the following `PostText` request to Amazon Lex\. 

      ```
      POST /bot/BookTrip/alias/$LATEST/user/wch89kjqcpkds8seny7dly5x3otq68j3/text
      "Content-Type":"application/json"
      "Content-Encoding":"amz-1.0"
      
      {
         "inputText":"yes",
         "sessionAttributes":{
            "confirmationContext":"AutoPopulate",
            "currentReservation":"{\"ReservationType\":\"Car\",
                                   \"PickUpCity\":null,
                                   \"PickUpDate\":null,
                                   \"ReturnDate\":null,
                                   \"CarType\":null}",
            "lastConfirmedReservation":"{\"ReservationType\":\"Hotel\",
                                         \"Location\":\"Chicago\",
                                         \"RoomType\":\"queen\",
                                         \"CheckInDate\":\"2016-12-18\",
                                         \"Nights\":\"5\"}"
         }
      }
      ```

   1. Amazon Lex reads the `inputText` and it knows the context \(asked the user to confirm the auto population\)\. Amazon Lex invokes the Lambda function by sending the following event:

      ```
      {
          "messageVersion": "1.0",
          "invocationSource": "DialogCodeHook",
          "userId": "wch89kjqcpkds8seny7dly5x3otq68j3",
          "sessionAttributes": {
              "confirmationContext": "AutoPopulate",
              "currentReservation": "{\"ReservationType\":\"Car\",\"PickUpCity\":null,\"PickUpDate\":null,\"ReturnDate\":null,\"CarType\":null}",
              "lastConfirmedReservation": "{\"ReservationType\":\"Hotel\",\"Location\":\"Chicago\",\"RoomType\":\"queen\",\"CheckInDate\":\"2016-12-18\",\"Nights\":\"5\"}"
          },
          "bot": {
              "name": "BookTrip",
              "alias": null,
              "version": "$LATEST"
          },
          "outputDialogMode": "Text",
          "currentIntent": {
              "name": "BookCar",
              "slots": {
                  "PickUpDate": "2016-12-18",
                  "ReturnDate": "2016-12-22",
                  "DriverAge": null,
                  "CarType": null,
                  "PickUpCity": "Chicago"
              },
              "confirmationStatus": "Confirmed"
          }
      }
      ```

      Because the user replied Yes, Amazon Lex sets the `confirmationStatus` to `Confirmed`\. 

   1. From the `confirmationStatus`, the Lambda function knows that the prepopulated values are correct\. The Lambda function does the following:
      + Updates the `currentReservation` session attribute to slot value it had prepopulated\.
      + Sets the `dialogAction.type` to `ElicitSlot`
      + Sets the `slotToElicit` value to `DriverAge`\. 

      The following response is sent:

      ```
      {
          "sessionAttributes": {
              "currentReservation": "{\"ReservationType\":\"Car\",\"PickUpCity\":\"Chicago\",\"PickUpDate\":\"2016-12-18\",\"ReturnDate\":\"2016-12-22\",\"CarType\":null}",
              "lastConfirmedReservation": "{\"ReservationType\":\"Hotel\",\"Location\":\"Chicago\",\"RoomType\":\"queen\",\"CheckInDate\":\"2016-12-18\",\"Nights\":\"5\"}"
          },
          "dialogAction": {
              "type": "ElicitSlot",
              "intentName": "BookCar",
              "slots": {
                  "PickUpDate": "2016-12-18",
                  "ReturnDate": "2016-12-22",
                  "DriverAge": null,
                  "CarType": null,
                  "PickUpCity": "Chicago"
              },
              "slotToElicit": "DriverAge",
              "message": {
                  "contentType": "PlainText",
                  "content": "How old is the driver of this car rental?"
              }
          }
      }
      ```

   1. Amazon Lex returns following response:  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lex/latest/dg/images/book-car-20.png)

      The client displays the message "How old is the driver of this car rental?" and the conversation continues\.