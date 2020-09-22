# AMAZON\.PhoneNumber<a name="built-in-slot-phone"></a>

Converts the numbers or words that represent a phone number into a string format without punctuation as follows\.


| Type | Description | Input | Result | 
| --- | --- | --- | --- | 
| International number with leading plus \(\+\) sign | 11\-digit number with leading plus sign\. | \+61 7 4445 1061 \+1 \(509\) 555\-1212 | `+61744431061` `+15095551212` | 
| International number without leading plus \(\+\) sign | 11\-digit number without leading plus sign | 1 \(509\) 555\-1212 61 7 4445 1061 | `15095551212` `61744451061` | 
| National number | 10\-digit number without international code | \(03\) 5115 4444 \(509\) 555\-1212 | `0351154444` `5095551212` | 
| Local number | 7\-digit phone number without an international code or an area code | 555\-1212 | 5551212 | 