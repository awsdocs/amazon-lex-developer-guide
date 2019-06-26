# Amazon Lex Resource\-Based Policy Example<a name="security_iam_resource-based-policy-examples"></a>

Resource\-based policies are JSON policy documents that specify what actions a specified principal can perform on the Amazon Lex resource and under what conditions\. To learn how to create a bot, see [Getting Started with Amazon Lex](getting-started.md)\.

## Allow a User to Manage a Specific Bot<a name="security_iam_resource-based-policy-examples-manage-one-bot"></a>

The following permissions policy grants the user permissions to build and test a pizza ordering bot\. It allows the user to use only the `OrderPizza` intent and `Toppings` slot type when editing the bot in the `us-east-2` Region\. 

The `Condition` block uses the `ForAllValues:StringEqualsIfExists` condition and the Amazon Lex `lex:associatedIntents` and `lex:associatedSlotType` condition keys to limit the intent and slot types that the user can use for this bot\.

```
{
    "Version": "2012-10-17",
    "Statement": [
       {
           "Effect": "Allow",
           "Action": [
                "lex:Create*Version",
                "lex:Post*",
                "lex:Put*",
                "lex:Delete*"
            ],
            "Resource": [
                "arn:aws:lex:us-east-2:*:bot:PizzaBot:*",
                "arn:aws:lex:us-east-2:*:intent:OrderPizza:*",
                "arn:aws:lex:us-east-2:*:slottype:Toppings:*"
            ],
            "Condition": {
                "ForAllValues:StringEqualsIfExists": {
                    "lex:associatedIntents": [
                        "OrderPizza"
                    ],
                    "lex:associatedSlotTypes": [
                        "Toppings"
                    ]
                }
            }
        },
        {
            "Effect": "Allow",
            "Action": [
                "lex:Get*"
            ],
            "Resource": [
                "arn:aws:lex:us-east-2:*:bot:*",
                "arn:aws:lex:us-east-2:*:intent:*",
                "arn:aws:lex:us-east-2:*:slottype:*"
            ]
        }
    ]
 }
```