# Step 1: Review the Blueprints Used in this Exercise<a name="ex-book-trip-blueprints"></a>

**Topics**
+ [Overview of the Bot Blueprint \(BookTrip\)](#ex-book-trip-bp-summary-bot)
+ [Overview of the Lambda Function Blueprint \(lex\-book\-trip\-python\)](#ex-book-trip-summary-lambda)

## Overview of the Bot Blueprint \(BookTrip\)<a name="ex-book-trip-bp-summary-bot"></a>

The blueprint \(**BookTrip**\) you use to create a bot provides the following preconfiguration:
+ **Slot types** – Two custom slot types:
  +  `RoomTypes` with enumeration values: `king`, `queen`, and `deluxe`, for use in the `BookHotel` intent\.
  +  `CarTypes` with enumeration values: `economy`, `standard`, `midsize`, `full size`, `luxury`, and `minivan`, for use in the `BookCar` intent\.

     
+ **Intent 1 \(BookHotel\)** – It is preconfigured as follows:
  + **Preconfigured slots** 
    + `RoomType`, of the `RoomTypes` custom slot type
    + `Location`, of the `AMAZON.US_CITY` built\-in slot type
    + `CheckInDate`, of the `AMAZON.DATE` built\-in slot type
    + `Nights`, of the `AMAZON.NUMBER` built\-in slot type
  + **Preconfigured utterances** 
    + "Book a hotel"
    + "I want to make hotel reservations" 
    + "Book a \{Nights\} stay in \{Location\}"

    If the user utters any of these, Amazon Lex determines that `BookHotel` is the intent and then prompts the user for slot data\.
  + **Preconfigured prompts** 
    + Prompt for the `Location` slot – "What city will you be staying in?"
    + Prompt for the `CheckInDate` slot – "What day do you want to check in?"
    + Prompt for the `Nights` slot – "How many nights will you be staying?" 
    + Prompt for the `RoomType` slot – "What type of room would you like, queen, king, or deluxe?" 
    + Confirmation statement – "Okay, I have you down for a \{Nights\} night stay in \{Location\} starting \{CheckInDate\}\. Shall I book the reservation?" 
    + Denial – "Okay, I have cancelled your reservation in progress\."

       
+ **Intent 2 \(BookCar\)** – It is preconfigured as follows:
  + **Preconfigured slots** 
    + `PickUpCity`, of the `AMAZON.US_CITY` built\-in type
    + `PickUpDate`, of the `AMAZON.DATE` built\-in type
    + `ReturnDate`, of the `AMAZON.DATE` built\-in type
    + `DriverAge`, of the `AMAZON.NUMBER` built\-in type
    + `CarType`, of the `CarTypes` custom type
  + **Preconfigured utterances** 
    + "Book a car"
    + "Reserve a car" 
    + "Make a car reservation"

    If the user utters any of these, Amazon Lex determines BookCar is the intent and then prompts the user for slot data\.
  + **Preconfigured prompts**
    + Prompt for the `PickUpCity` slot – "In what city do you need to rent a car?"
    + Prompt for the `PickUpDate` slot – "What day do you want to start your rental?""
    + Prompt for the `ReturnDate` slot – "What day do you want to return this car?"
    + Prompt for the `DriverAge` slot – "How old is the driver for this rental?"
    + Prompt for the `CarType` slot – "What type of car would you like to rent? Our most popular options are economy, midsize, and luxury"
    + Confirmation statement – "Okay, I have you down for a \{CarType\} rental in \{PickUpCity\} from \{PickUpDate\} to \{ReturnDate\}\. Should I book the reservation?" 
    + Denial – "Okay, I have cancelled your reservation in progress\."

## Overview of the Lambda Function Blueprint \(lex\-book\-trip\-python\)<a name="ex-book-trip-summary-lambda"></a>

In addition to the bot blueprint, AWS Lambda provides a blueprint \(**lex\-book\-trip\-python**\) that you can use as a code hook with the bot blueprint\. For a list of bot blueprints and corresponding Lambda function blueprints, see [Amazon Lex and AWS Lambda Blueprints](lex-lambda-blueprints.md)\.

When you create a bot using the BookTrip blueprint, you update configuration of both the intents \(BookCar and BookHotel\) by adding this Lambda function as a code hook for both initialization/validation of user data input and fulfillment of the intents\.

This Lambda function code provided showcases dynamic conversation using previously known information \(persisted in session attributes\) about a user to initialize slot values for an intent\. For more information, see [Managing Conversation Context](context-mgmt.md)\.

**Next Step**  
[Step 2: Create an Amazon Lex Bot ](ex-book-trip-create-bot.md)