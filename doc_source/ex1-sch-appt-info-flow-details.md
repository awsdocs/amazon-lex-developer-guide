# Details of Information Flow<a name="ex1-sch-appt-info-flow-details"></a>

The `ScheduleAppointment` bot blueprint primarily showcases the use of dynamically generated response cards\. The Lambda function in this exercise includes response cards in its response to Amazon Lex\. Amazon Lex includes the response cards in its reply to the client\. This section explains both the following:
+ Data flow between client and Amazon Lex\.

   

  The section assumes client sends requests to Amazon Lex using the `PostText` runtime API and shows request/response details accordingly\. For more information about the `PostText` runtime API, see [PostText](API_runtime_PostText.md)\.
**Note**  
For an example of information flow between client and Amazon Lex in which client uses the `PostContent` API, see [Step 2a \(Optional\): Review the Details of the Spoken Information Flow \(Console\) ](gs-bp-details-postcontent-flow.md)\.

   
+ Data flow between Amazon Lex and the Lamba function\. For more information, see [Lambda Function Input Event and Response Format](lambda-input-response-format.md)\.

**Note**  
The example assumes that you are using the Facebook Messenger client, which does not pass session attributes in the request to Amazon Lex\. Accordingly, the example requests shown in this section show empty `sessionAttributes`\. If you test the bot using the client provided in the Amazon Lex console, the client includes the session attributes\.

This section describes what happens after each user input\.

1. User: Types **Book an appointment**\.

   1. The client \(console\) sends the following [PostContent](API_runtime_PostContent.md) request to Amazon Lex:

      ```
      POST /bot/ScheduleAppointment/alias/$LATEST/user/bijt6rovckwecnzesbthrr1d7lv3ja3n/text
      "Content-Type":"application/json"
      "Content-Encoding":"amz-1.0"
      
      {
         "inputText":"book appointment",
         "sessionAttributes":{}
      }
      ```

      Both the request URI and the body provide information to Amazon Lex:
      + Request URI – Provides the bot name \(ScheduleAppointment\), the bot alias \($LATEST\), and the user name ID\. The trailing `text` indicates that it is a `PostText` \(not `PostContent`\) API request\.
      + Request body – Includes the user input \(`inputText`\) and empty `sessionAttributes`\. 

   1. From the `inputText`, Amazon Lex detects the intent \(`MakeAppointment`\)\. The service invokes the Lambda function, which is configured as a code hook, to perform initialization and validation by passing the following event\. For details, see [Input Event Format](lambda-input-response-format.md#using-lambda-input-event-format)\.

      ```
      {
          "currentIntent": {
              "slots": {
                  "AppointmentType": null,
                  "Date": null,
                  "Time": null
              },
              "name": "MakeAppointment",
              "confirmationStatus": "None"
          },
          "bot": {
              "alias": null,
              "version": "$LATEST",
              "name": "ScheduleAppointment"
          },
          "userId": "bijt6rovckwecnzesbthrr1d7lv3ja3n",
          "invocationSource": "DialogCodeHook",
          "outputDialogMode": "Text",
          "messageVersion": "1.0",
          "sessionAttributes": {}
      }
      ```

      In addition to the information sent by the client, Amazon Lex also includes the following data:
      + `currentIntent` – Provides current intent information\.
      + `invocationSource` – Indicates the purpose of the Lambda function invocation\. In this case, the purpose is to perform user data initialization and validation\. \(Amazon Lex knows that the user has not provided all of the slot data to fulfill the intent yet\.\)
      + `messageVersion` – Currently Amazon Lex supports only the 1\.0 version\. 

   1. At this time, all of the slot values are null \(there is nothing to validate\)\. The Lambda function returns the following response to Amazon Lex, directing the service to elicit information for the `AppointmentType` slot\. For information about the response format, see [Response Format](lambda-input-response-format.md#using-lambda-response-format)\. 

      ```
      {
          "dialogAction": {
              "slotToElicit": "AppointmentType",
              "intentName": "MakeAppointment",
              "responseCard": {
                  "genericAttachments": [
                      {
                          "buttons": [
                              {
                                  "text": "cleaning (30 min)",
                                  "value": "cleaning"
                              },
                              {
                                  "text": "root canal (60 min)",
                                  "value": "root canal"
                              },
                              {
                                  "text": "whitening (30 min)",
                                  "value": "whitening"
                              }
                          ],
                          "subTitle": "What type of appointment would you like to schedule?",
                          "title": "Specify Appointment Type"
                      }
                  ],
                  "version": 1,
                  "contentType": "application/vnd.amazonaws.card.generic"
              },
              "slots": {
                  "AppointmentType": null,
                  "Date": null,
                  "Time": null
              },
              "type": "ElicitSlot",
              "message": {
                  "content": "What type of appointment would you like to schedule?",
                  "contentType": "PlainText"
              }
          },
          "sessionAttributes": {}
      }
      ```

      The response includes the `dialogAction` and `sessionAttributes` fields\. Among other things, the `dialogAction` field returns the following fields: 
      + `type` – By setting this field to `ElicitSlot`, the Lambda function directs Amazon Lex to elicit the value for the slot specified in the `slotToElicit` field\. The Lambda function also provides a `message` to convey to the user\.
      + `responseCard` – Identifies a list of possible values for the `AppointmentType` slot\. A client that supports response cards \(for example, the Facebook Messenger\) displays a response card to allow the user to choose an appointment type, as follows:  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lex/latest/dg/images/respcard-10.png)

   1. As indicated by the `dialogAction.type` in the response from the Lambda function, Amazon Lex sends the following response back to the client:   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lex/latest/dg/images/appt-10.png)

      The client reads the response, and then displays the message: "What type of appointment would you like to schedule?" and the response card \(if the client supports response cards\)\.

1. User: Depending on the client, the user has two options:
   + If the response card is shown, choose **root canal \(60 min\)** or type **root canal**\.
   + If the client does not support response cards, type **root canal**\.

   1. The client sends the following `PostText` request to Amazon Lex \(line breaks have been added for readability\):

      ```
      POST /bot/BookTrip/alias/$LATEST/user/bijt6rovckwecnzesbthrr1d7lv3ja3n/text
      "Content-Type":"application/json"
      "Content-Encoding":"amz-1.0"
      
      {
         "inputText": "root canal",
          "sessionAttributes": {}
      }
      ```

   1. Amazon Lex invokes the Lambda function for user data validation by sending the following event as a parameter:

      ```
      {
          "currentIntent": {
              "slots": {
                  "AppointmentType": "root canal",
                  "Date": null,
                  "Time": null
              },
              "name": "MakeAppointment",
              "confirmationStatus": "None"
          },
          "bot": {
              "alias": null,
              "version": "$LATEST",
              "name": "ScheduleAppointment"
          },
          "userId": "bijt6rovckwecnzesbthrr1d7lv3ja3n",
          "invocationSource": "DialogCodeHook",
          "outputDialogMode": "Text",
          "messageVersion": "1.0",
          "sessionAttributes": {}
      }
      ```

      In the event data, note the following:
      + `invocationSource` continues to be `DialogCodeHook`\. In this step, we are just validating user data\.
      + Amazon Lex sets the `AppointmentType` field in the `currentIntent.slots` slot to `root canal`\.
      + Amazon Lex simply passes the `sessionAttributes` field between the client and the Lambda function\.

   1. The Lambda function validates the user input and returns the following response to Amazon Lex, directing the service to elicit a value for the appointment date\.

      ```
      {
          "dialogAction": {
              "slotToElicit": "Date",
              "intentName": "MakeAppointment",
              "responseCard": {
                  "genericAttachments": [
                      {
                          "buttons": [
                              {
                                  "text": "2-15 (Wed)",
                                  "value": "Wednesday, February 15, 2017"
                              },
                              {
                                  "text": "2-16 (Thu)",
                                  "value": "Thursday, February 16, 2017"
                              },
                              {
                                  "text": "2-17 (Fri)",
                                  "value": "Friday, February 17, 2017"
                              },
                              {
                                  "text": "2-20 (Mon)",
                                  "value": "Monday, February 20, 2017"
                              },
                              {
                                  "text": "2-21 (Tue)",
                                  "value": "Tuesday, February 21, 2017"
                              }
                          ],
                          "subTitle": "When would you like to schedule your root canal?",
                          "title": "Specify Date"
                      }
                  ],
                  "version": 1,
                  "contentType": "application/vnd.amazonaws.card.generic"
              },
              "slots": {
                  "AppointmentType": "root canal",
                  "Date": null,
                  "Time": null
              },
              "type": "ElicitSlot",
              "message": {
                  "content": "When would you like to schedule your root canal?",
                  "contentType": "PlainText"
              }
          },
          "sessionAttributes": {}
      }
      ```

      Again, the response includes the `dialogAction` and `sessionAttributes` fields\. Among other things, the `dialogAction` field returns the following fields: 
      + `type` – By setting this field to `ElicitSlot`, the Lambda function directs Amazon Lex to elicit the value for the slot specified in the `slotToElicit` field\. The Lambda function also provides a `message` to convey to the user\.
      + `responseCard` – Identifies a list of possible values for the `Date` slot\. A client that supports response cards \(for example, Facebook Messenger\) displays a response card that allows the user to choose an appointment date:  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lex/latest/dg/images/respcard-20.png)

        Although the Lambda function returned five dates, the client \(Facebook Messenger\) has a limit of three buttons for a response card\. Therefore, you see only the first three values in the screen shot\.

        These dates are hard coded in the Lambda function\. In a production application, you might use a calendar to get available dates in real time\. Because the dates are dynamic, you must generate the response card dynamically in the Lambda function\.

   1. Amazon Lex notices the `dialogAction.type` and returns a response to the client that includes information from the Lambda function's response\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lex/latest/dg/images/appt-20.png)

      The client displays the message: **When would you like to schedule your root canal?** and the response card \(if the client supports response cards\)\.

1. User: Types **Thursday**\.

   1. The client sends the following `PostText` request to Amazon Lex \(line breaks have been added for readability\):

      ```
      POST /bot/BookTrip/alias/$LATEST/user/bijt6rovckwecnzesbthrr1d7lv3ja3n/text
      "Content-Type":"application/json"
      "Content-Encoding":"amz-1.0"
      
      {
         "inputText": "Thursday",
          "sessionAttributes": {}
      }
      ```

   1. Amazon Lex invokes the Lambda function for user data validation by sending in the following event as a parameter:

      ```
      {
          "currentIntent": {
              "slots": {
                  "AppointmentType": "root canal",
                  "Date": "2017-02-16",
                  "Time": null
              },
              "name": "MakeAppointment",
              "confirmationStatus": "None"
          },
          "bot": {
              "alias": null,
              "version": "$LATEST",
              "name": "ScheduleAppointment"
          },
          "userId": "u3fpr9gghj02zts7y5tpq5mm4din2xqy",
          "invocationSource": "DialogCodeHook",
          "outputDialogMode": "Text",
          "messageVersion": "1.0",
          "sessionAttributes": {}
      }
      ```

      In the event data, note the following:
      + `invocationSource` continues to be `DialogCodeHook`\. In this step, we are just validating the user data\.
      + Amazon Lex sets the `Date` field in the `currentIntent.slots` slot to `2017-02-16`\.
      + Amazon Lex simply passes the `sessionAttributes` between the client and the Lambda function\.

   1. The Lambda function validates the user input\. This time the Lambda function determines that there are no appointments available on the specified date\. It returns the following response to Amazon Lex, directing the service to again elicit a value for the appointment date\.

      ```
      {
          "dialogAction": {
              "slotToElicit": "Date",
              "intentName": "MakeAppointment",
              "responseCard": {
                  "genericAttachments": [
                      {
                          "buttons": [
                              {
                                  "text": "2-15 (Wed)",
                                  "value": "Wednesday, February 15, 2017"
                              },
                              {
                                  "text": "2-17 (Fri)",
                                  "value": "Friday, February 17, 2017"
                              },
                              {
                                  "text": "2-20 (Mon)",
                                  "value": "Monday, February 20, 2017"
                              },
                              {
                                  "text": "2-21 (Tue)",
                                  "value": "Tuesday, February 21, 2017"
                              }
                          ],
                          "subTitle": "When would you like to schedule your root canal?",
                          "title": "Specify Date"
                      }
                  ],
                  "version": 1,
                  "contentType": "application/vnd.amazonaws.card.generic"
              },
              "slots": {
                  "AppointmentType": "root canal",
                  "Date": null,
                  "Time": null
              },
              "type": "ElicitSlot",
              "message": {
                  "content": "We do not have any availability on that date, is there another day which works for you?",
                  "contentType": "PlainText"
              }
          },
          "sessionAttributes": {
           "bookingMap": "{\"2017-02-16\": []}"
         }
      }
      ```

      Again, the response includes the `dialogAction` and `sessionAttributes` fields\. Among other things, the `dialogAction` returns the following fields: 
      + `dialogAction` field:
        + `type` – The Lambda function sets this value to `ElicitSlot` and resets the `slotToElicit` field to `Date`\. The Lambda function also provides an appropriate `message` to convey to the user\.
        + `responseCard` – Returns a list of values for the `Date` slot\.
      + `sessionAttributes` \- This time the Lambda function includes the `bookingMap` session attribute\. Its value is the requested date of the appointment and available appointments \(an empty object indicates that no appointments are available\)\.

   1. Amazon Lex notices the `dialogAction.type` and returns a response to the client that includes information from the Lambda function's response\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lex/latest/dg/images/appt-30.png)

      The client displays the message: **We do not have any availability on that date, is there another day which works for you?** and the response card \(if the client supports response cards\)\.

1. User: Depending on the client, the user has two options:
   + If the response card is shown, choose **2\-15 \(Wed\)** or type **Wednesday**\.
   + If the client does not support response cards, type **Wednesday**\.

   1. The client sends the following `PostText` request to Amazon Lex:

      ```
      POST /bot/BookTrip/alias/$LATEST/user/bijt6rovckwecnzesbthrr1d7lv3ja3n/text
      "Content-Type":"application/json"
      "Content-Encoding":"amz-1.0"
      
      {
         "inputText": "Wednesday",
          "sessionAttributes": {
         }
      }
      ```
**Note**  
The Facebook Messenger client does not set any session attributes\. If you want to maintain session states between requests, you must do so in the Lambda function\. In a real application, you might need to maintain these session attributes in a backend database\.

   1. Amazon Lex invokes the Lambda function for user data validation by sending the following event as a parameter:

      ```
      {
          "currentIntent": {
              "slots": {
                  "AppointmentType": "root canal",
                  "Date": "2017-02-15",
                  "Time": null
              },
              "name": "MakeAppointment",
              "confirmationStatus": "None"
          },
          "bot": {
              "alias": null,
              "version": "$LATEST",
              "name": "ScheduleAppointment"
          },
          "userId": "u3fpr9gghj02zts7y5tpq5mm4din2xqy",
          "invocationSource": "DialogCodeHook",
          "outputDialogMode": "Text",
          "messageVersion": "1.0",
          "sessionAttributes": {
          }
      }
      ```

      Amazon Lex updated `currentIntent.slots` by setting the `Date` slot to `2017-02-15`\. 

   1. The Lambda function validates the user input and returns the following response to Amazon Lex, directing it to elicit the value for the appointment time\. 

      ```
      {
          "dialogAction": {
              "slots": {
                  "AppointmentType": "root canal",
                  "Date": "2017-02-15",
                  "Time": "16:00"
              },
              "message": {
                  "content": "What time on 2017-02-15 works for you? 4:00 p.m. is our only availability, does that work for you?",
                  "contentType": "PlainText"
              },
              "type": "ConfirmIntent",
              "intentName": "MakeAppointment",
              "responseCard": {
                  "genericAttachments": [
                      {
                          "buttons": [
                              {
                                  "text": "yes",
                                  "value": "yes"
                              },
                              {
                                  "text": "no",
                                  "value": "no"
                              }
                          ],
                          "subTitle": "Is 4:00 p.m. on 2017-02-15 okay?",
                          "title": "Confirm Appointment"
                      }
                  ],
                  "version": 1,
                  "contentType": "application/vnd.amazonaws.card.generic"
              }
          },
          "sessionAttributes": {
              "bookingMap": "{\"2017-02-15\": [\"10:00\", \"16:00\", \"16:30\"]}"
          }
      }
      ```

      Again, the response includes the `dialogAction` and `sessionAttributes` fields\. Among other things, the `dialogAction` returns the following fields: 
      + `dialogAction` field:
        + `type` – The `Lambda` function sets this value to `ConfirmIntent`, directing Amazon Lex to obtain user confirmation of the appointment time suggested in the `message`\.
        + `responseCard` – Returns a list of yes/no values for the user to choose from\. If the client supports response cards, it displays the response card, as shown in the following example:  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lex/latest/dg/images/respcard-30.png)
      + `sessionAttributes` \- The Lambda function sets the `bookingMap` session attribute with its value set to the appointment date and available appointments on that date\. In this example, these are 30\-minute appointments\. For a root canal that requires one hour, only 4 p\.m\. can be booked\.

   1. As indicated in the `dialogAction.type` in the Lambda function's response, Amazon Lex returns the following response to the client:   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/lex/latest/dg/images/appt-40.png)

      The client displays the message: **What time on 2017\-02\-15 works for you? 4:00 p\.m\. is our only availability, does that work for you?**

1. User: Choose **yes**\. 

   Amazon Lex invokes the Lambda function with the following event data\. Because the user replied **yes**, Amazon Lex sets the `confirmationStatus` to `Confirmed`, and sets the `Time` field in `currentIntent.slots ` to `4 p.m`\.

   ```
   {
       "currentIntent": {
           "slots": {
               "AppointmentType": "root canal",
               "Date": "2017-02-15",
               "Time": "16:00"
           },
           "name": "MakeAppointment",
           "confirmationStatus": "Confirmed"
       },
       "bot": {
           "alias": null,
           "version": "$LATEST",
           "name": "ScheduleAppointment"
       },
       "userId": "u3fpr9gghj02zts7y5tpq5mm4din2xqy",
       "invocationSource": "FulfillmentCodeHook",
       "outputDialogMode": "Text",
       "messageVersion": "1.0",
       "sessionAttributes": {
      }
   }
   ```

   Because the `confirmationStatus` is confirmed, the Lambda function processes the intent \(books a dental appointment\) and returns the following response to Amazon Lex: 

   ```
   {
       "dialogAction": {
           "message": {
               "content": "Okay, I have booked your appointment.  We will see you at 4:00 p.m. on 2017-02-15",
               "contentType": "PlainText"
           },
           "type": "Close",
           "fulfillmentState": "Fulfilled"
       },
       "sessionAttributes": {
           "formattedTime": "4:00 p.m.",
           "bookingMap": "{\"2017-02-15\": [\"10:00\"]}"
       }
   }
   ```

   Note the following:
   + The Lambda function has updated the `sessionAttributes`\.
   + `dialogAction.type` is set to `Close`, which directs Amazon Lex to not expect a user response\. 
   + `dialogAction.fulfillmentState` is set to `Fulfilled`, indicating that the intent is successfully fulfilled\.

   The client displays the message: **Okay, I have booked your appointment\. We will see you at 4:00 p\.m\. on 2017\-02\-15**\.