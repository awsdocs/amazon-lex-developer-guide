# AMAZON\.PhoneNumber<a name="built-in-slot-phone"></a>


|  | 
| --- |
| This slot type is in preview release for Amazon Lex and is subject to change\. | 

Converts the numbers or words that represent a phone number into a string format without punctuation as follows\.

**Note**  
Only U\.S\. phone numbers are supported\.

 


| Type | Description | Input | Result | 
| --- | --- | --- | --- | 
| International number with leading plus \(\+\) sign | 11\-digit number with leading plus sign\. | \+1 509 555\-1212 | \+15095551212 | 
| International number without leading plus \(\+\) sign | 11\-digit number without leading plus sign | 1 \(509\) 555\-1212 | 15095551212 | 
| National number | 10\-digit number without international code | \(509\) 555\-1212 | 5095551212 | 
| Local number | 7\-digit phone number without an international code or an area code | 555\-1212 | 5551212 | 