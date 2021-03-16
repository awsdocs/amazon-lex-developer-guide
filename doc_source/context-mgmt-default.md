# Using Default Slot Values<a name="context-mgmt-default"></a>

When you use a default value, you specify a source for a slot value to be filled for new intents when no slot is provided by the user’s input\. This source can be previous dialog, request or session attributes, or a fixed value that you set at build\-time\. 

You can use the following as the source for your default values\.
+ Previous dialog \(contexts\) – \#context\-name\.parameter\-name
+ Session attributes – \[attribute\-name\]
+ Request attributes – <attribute\-name>
+ Fixed value – Any value that doesn't match the previous

When you use the [PutIntent](API_PutIntent.md) operation to add slots to an intent, you can add a list of default values\. Default values are used in the order that they are listed\. For example, suppose you have an intent with a slot with the following definition:

```
"slots": [
    {
        "name": "reservation-start-date",
        "defaultValueSpec": {
            "defaultValueList": [
                {
                    "defaultValue": "#book-car-fulfilled.startDate"
                },
                {  
                    "defaultValue": "[reservationStartDate]"
                }
            ]
        },
        Other slot configuration settings
    }
]
```

When the intent is recognized, the slot named "reservation\-start\-date" has its value set to one of the following\.

1. If the "book\-car\-fulfilled" context is active, the value of the "startDate" parameter is used as the default value\.

1. If the "book\-car\-fulfilled" context is not active, or if the "startDate" parameter is not set, the value of the "reservationStartDate" session attribute is used as the default value\.

1. If neither of the first two default values are used, then the slot doesn't have a default value and Amazon Lex will elicit a value as usual\.

If a default value is used for the slot, the slot is not elicited even if it is required\.