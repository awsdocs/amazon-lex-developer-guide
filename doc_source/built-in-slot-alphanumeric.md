# AMAZON\.AlphaNumeric<a name="built-in-slot-alphanumeric"></a>

Recognizes strings made up of letters and numbers, such as **APQ123**\.

You can use the `AMAZON.AlphaNumeric` slot type for strings that contain: 
+ Alphabetical characters, such as **ABC**
+ Numeric characters, such as **123**
+ A combination of alphanumeric characters, such as **ABC123**

You can add a regular expression to the `AMAZON.AlphaNumeric` slot type to validate values entered for the slot\. For example, you can use a regular expression to validate:
+ United Kingdom or Canadian postal codes
+ Driver's license numbers
+ Vehicle identification numbers

Use a standard regular expression\. Amazon Lex supports the following characters in the regular expression:
+ A\-Z, a\-z
+ 0\-9

Amazon Lex also supports Unicode characters in regular expressions\. The form is `\uUnicode`\. Use four digits to represent Unicode characters\. For example, `[\u0041-\u005A]` is equivalent to \[A\-Z\]\.

The following regular expression operators are not supported:
+ Infinite repeaters: \*, \+, or \{x,\} with no upper bound\.
+ Wild card \(\.\)

The maximum length of the regular expression is 100 characters\. The maximum length of a string stored in an AMAZON\.AlphaNumeric slot type that uses a regular expression is 30 characters\.

The following are some example regular expressions\.
+ Alphanumeric strings, such as **APQ123** or **APQ1**: `[A-Z]{3}[0-9]{1,3}` or a more constrained `[A-DP-T]{3} [1-5]{1,3}`
+ US Postal Service Priority Mail International format, such as **CP123456789US**: `CP[0-9]{9}US`
+ Bank routing numbers, such as **123456789**: `[0-9]{9}`

To set the regular expression for a slot type, use the console or the [PutSlotType](API_PutSlotType.md) operation\. The regular expression is validated when you save the slot type\. If the expression isn't valid, Amazon Lex returns an error message\.

When you use a regular expression in a slot type, Amazon Lex checks input to slots of that type against the regular expression\. If the input matches the expression, the value is accepted for the slot\. If the input does not match, Amazon Lex prompts the user to repeat the input\. 