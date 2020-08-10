# Step 2a \(Optional\): Review the Details of the Spoken Information Flow \(Console\)<a name="gs-bp-details-postcontent-flow"></a>

This section explains the flow of information between the client and Amazon Lex when the client uses speech to send requests\. For more information, see [PostContent](API_runtime_PostContent.md)\. 

1. The user says: I would like to order some flowers\.

   1. The client \(console\) sends the following [PostContent](API_runtime_PostContent.md) request to Amazon Lex: 

      ```
      POST /bot/OrderFlowers/alias/$LATEST/user/4o9wwdhx6nlheferh6a73fujd3118f5w/content HTTP/1.1
      x-amz-lex-session-attributes: "e30=" 
      Content-Type: "audio/x-l16; sample-rate=16000; channel-count=1"
      Accept: "audio/mpeg"
      
      
      Request body
      input stream
      ```

      Both the request URI and the body provide information to Amazon Lex:
      + Request URI – Provides the bot name \(`OrderFlowers`\), bot alias \(`$LATEST`\), and the user name \(a random string that identifies the user\)\. `content` indicates that this is a `PostContent` API request \(not a `PostText` request\)\.
      + Request headers
        + `x-amz-lex-session-attributes` – The base64\-encoded value represents "\{\}"\. When the client makes the first request, there are no session attributes\. 
        + `Content-Type` – Reflects the audio format\.
      + Request body – The user input audio stream \("I would like to order some flowers\."\)\.
**Note**  
If the user chooses to send text \("I would like to order some flowers"\) to the `PostContent` API instead of speaking, the request body is the user input\. The `Content-Type` header is set accordingly:  

      ```
      POST /bot/OrderFlowers/alias/$LATEST/user/4o9wwdhx6nlheferh6a73fujd3118f5w/content HTTP/1.1
      x-amz-lex-session-attributes: "e30="
      Content-Type: "text/plain; charset=utf-8"
      Accept: accept
      
      Request body
      input stream
      ```

   1. From the input stream, Amazon Lex detects the intent \(`OrderFlowers`\)\. It then chooses one of the intent's slots \(in this case, the `FlowerType`\) and one of its value elicitation prompts, and then sends a response with the following headers: 

      ```
      x-amz-lex-dialog-state:ElicitSlot
      x-amz-lex-input-transcript:I would like to order some flowers.
      x-amz-lex-intent-name:OrderFlowers
      x-amz-lex-message:What type of flowers would you like to order?
      x-amz-lex-session-attributes:e30=
      x-amz-lex-slot-to-elicit:FlowerType
      x-amz-lex-slots:eyJQaWNrdXBUaW1lIjpudWxsLCJGbG93ZXJUeXBlIjpudWxsLCJQaWNrdXBEYXRlIjpudWxsfQ==
      ```

      The header values provide the following information:
      + `x-amz-lex-input-transcript` – Provides the transcript of the audio \(user input\) from the request
      + `x-amz-lex-message` – Provides the transcript of the audio Amazon Lex returned in the response
      + `x-amz-lex-slots` – The base64 encoded version of the slots and values:

        ```
        {"PickupTime":null,"FlowerType":null,"PickupDate":null}
        ```
      + `x-amz-lex-session-attributes` – The base64\-encoded version of the session attributes \(\{\}\)

      The client plays the audio in the response body\.

1. The user says: roses

   1. The client \(console\) sends the following [PostContent](API_runtime_PostContent.md) request to Amazon Lex: 

      ```
      POST /bot/OrderFlowers/alias/$LATEST/user/4o9wwdhx6nlheferh6a73fujd3118f5w/content HTTP/1.1
      x-amz-lex-session-attributes: "e30="
      Content-Type: "audio/x-l16; sample-rate=16000; channel-count=1" 
      Accept: "audio/mpeg"
      
      
      Request body
      input stream ("roses")
      ```

      The request body is the user input audio stream \(roses\)\. The `sessionAttributes` remains empty\.

   1. Amazon Lex interprets the input stream in the context of the current intent \(it remembers that it had asked this user for information pertaining to the `FlowerType` slot\)\. Amazon Lex first updates the slot value for the current intent\. It then chooses another slot \(`PickupDate`\), along with one of its prompt messages \(When do you want to pick up the roses?\), and returns a response with the following headers:

      ```
      x-amz-lex-dialog-state:ElicitSlot
      x-amz-lex-input-transcript:roses
      x-amz-lex-intent-name:OrderFlowers
      x-amz-lex-message:When do you want to pick up the roses?
      x-amz-lex-session-attributes:e30=
      x-amz-lex-slot-to-elicit:PickupDate
      x-amz-lex-slots:eyJQaWNrdXBUaW1lIjpudWxsLCJGbG93ZXJUeXBlIjoicm9zaSdzIiwiUGlja3VwRGF0ZSI6bnVsbH0=
      ```

      The header values provide the following information:
      + `x-amz-lex-slots` – The base64\-encoded version of the slots and values:

        ```
        {"PickupTime":null,"FlowerType":"roses","PickupDate":null}
        ```
      + `x-amz-lex-session-attributes` – The base64\-encoded version of the session attributes \(\{\}\)

      The client plays the audio in the response body\.

1. The user says: tomorrow

   1. The client \(console\) sends the following [PostContent](API_runtime_PostContent.md) request to Amazon Lex: 

      ```
      POST /bot/OrderFlowers/alias/$LATEST/user/4o9wwdhx6nlheferh6a73fujd3118f5w/content HTTP/1.1
      x-amz-lex-session-attributes: "e30="
      Content-Type: "audio/x-l16; sample-rate=16000; channel-count=1"
      Accept: "audio/mpeg"
      
      
      Request body
      input stream ("tomorrow")
      ```

      The request body is the user input audio stream \("tomorrow"\)\.The `sessionAttributes` remains empty\.

   1. Amazon Lex interprets the input stream in the context of the current intent \(it remembers that it had asked this user for information pertaining to the `PickupDate` slot\)\. Amazon Lex updates the slot \(`PickupDate`\) value for the current intent\. It then chooses another slot to elicit value for \(`PickupTime`\) and one of the value elicitation prompts \(When do you want to pick up the roses on 2017\-03\-18?\), and returns a response with the following headers:

      ```
      x-amz-lex-dialog-state:ElicitSlot
      x-amz-lex-input-transcript:tomorrow
      x-amz-lex-intent-name:OrderFlowers
      x-amz-lex-message:When do you want to pick up the roses on 2017-03-18?
      x-amz-lex-session-attributes:e30=
      x-amz-lex-slot-to-elicit:PickupTime
      x-amz-lex-slots:eyJQaWNrdXBUaW1lIjpudWxsLCJGbG93ZXJUeXBlIjoicm9zaSdzIiwiUGlja3VwRGF0ZSI6IjIwMTctMDMtMTgifQ==
      x-amzn-RequestId:3a205b70-0b69-11e7-b447-eb69face3e6f
      ```

      The header values provide the following information:
      + `x-amz-lex-slots` – The base64\-encoded version of the slots and values:

        ```
        {"PickupTime":null,"FlowerType":"roses","PickupDate":"2017-03-18"}
        ```
      + `x-amz-lex-session-attributes` – The base64\-encoded version of the session attributes \(\{\}\)

      The client plays the audio in the response body\.

1. The user says: 6 pm

   1. The client \(console\) sends the following [PostContent](API_runtime_PostContent.md) request to Amazon Lex: 

      ```
      POST /bot/OrderFlowers/alias/$LATEST/user/4o9wwdhx6nlheferh6a73fujd3118f5w/content HTTP/1.1
      x-amz-lex-session-attributes: "e30="
      Content-Type: "text/plain; charset=utf-8"
      Accept: "audio/mpeg"
      
      
      Request body
      input stream ("6 pm")
      ```

      The request body is the user input audio stream \("6 pm"\)\. The `sessionAttributes` remains empty\.

   1. Amazon Lex interprets the input stream in the context of the current intent \(it remembers that it had asked this user for information pertaining to the `PickupTime` slot\)\. It first updates the slot value for the current intent\. 

      Now Amazon Lex detects that it has information for all of the slots\. However, the `OrderFlowers` intent is configured with a confirmation message\. Therefore, Amazon Lex needs an explicit confirmation from the user before it can proceed to fulfill the intent\. It sends a response with the following headers requesting confirmation before ordering the flowers:

      ```
      x-amz-lex-dialog-state:ConfirmIntent
      x-amz-lex-input-transcript:six p. m.
      x-amz-lex-intent-name:OrderFlowers
      x-amz-lex-message:Okay, your roses will be ready for pickup by 18:00 on 2017-03-18.  Does this sound okay?
      x-amz-lex-session-attributes:e30=
      x-amz-lex-slots:eyJQaWNrdXBUaW1lIjoiMTg6MDAiLCJGbG93ZXJUeXBlIjoicm9zaSdzIiwiUGlja3VwRGF0ZSI6IjIwMTctMDMtMTgifQ==
      x-amzn-RequestId:083ca360-0b6a-11e7-b447-eb69face3e6f
      ```

      The header values provide the following information:
      + `x-amz-lex-slots` – The base64\-encoded version of the slots and values:

        ```
        {"PickupTime":"18:00","FlowerType":"roses","PickupDate":"2017-03-18"}
        ```
      + `x-amz-lex-session-attributes` – The base64\-encoded version of the session attributes \(\{\}\)

      The client plays the audio in the response body\.

1. The user says: Yes

   1. The client \(console\) sends the following [PostContent](API_runtime_PostContent.md) request to Amazon Lex: 

      ```
      POST /bot/OrderFlowers/alias/$LATEST/user/4o9wwdhx6nlheferh6a73fujd3118f5w/content HTTP/1.1
      x-amz-lex-session-attributes: "e30="
      Content-Type: "audio/x-l16; sample-rate=16000; channel-count=1"
      Accept: "audio/mpeg"
      
      
      Request body
      input stream ("Yes")
      ```

      The request body is the user input audio stream \("Yes"\)\. The `sessionAttributes` remains empty\.

   1. Amazon Lex interprets the input stream and understands that the user want to proceed with the order\. The `OrderFlowers` intent is configured with `ReturnIntent` as the fulfillment activity\. This directs Amazon Lex to return all of the intent data to the client\. Amazon Lex returns a response with following: 

      ```
      x-amz-lex-dialog-state:ReadyForFulfillment
      x-amz-lex-input-transcript:yes
      x-amz-lex-intent-name:OrderFlowers
      x-amz-lex-session-attributes:e30=
      x-amz-lex-slots:eyJQaWNrdXBUaW1lIjoiMTg6MDAiLCJGbG93ZXJUeXBlIjoicm9zaSdzIiwiUGlja3VwRGF0ZSI6IjIwMTctMDMtMTgifQ==
      ```

      The`x-amz-lex-dialog-state` response header is set to `ReadyForFulfillment`\. The client can then fulfill the intent\.

1. Now, retest the bot\. To establish a new \(user\) context, choose the **Clear** link in the console\. Provide data for the `OrderFlowers` intent, and include some invalid data\. For example: 
   + Jasmine as the flower type \(it is not one of the supported flower types\)
   + Yesterday as the day when you want to pick up the flowers

   Notice that the bot accepts these values because you don't have any code to initialize and validate the user data\. In the next section, you add a Lambda function to do this\. Note the following about the Lambda function:
   + It validates slot data after every user input\. It fulfills the intent at the end\. That is, the bot processes the flower order and returns a message to the user instead of simply returning slot data to the client\. For more information, see [Using Lambda Functions](using-lambda.md)\.
   + It also sets the session attributes\. For more information about session attributes, see [PostText](API_runtime_PostText.md)\. 

      After you complete the Getting Started section, you can do the additional exercises \([Additional Examples: Creating Amazon Lex Bots](additional-exercises.md) \)\. [Example: BookTrip](ex-book-trip.md) uses session attributes to share cross\-intent information to engage in a dynamic conversation with the user\.

**Next Step**  
[Step 3: Create a Lambda Function \(Console\)](gs-bp-create-lambda-function.md)