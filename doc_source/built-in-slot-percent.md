# AMAZON\.Percentage<a name="built-in-slot-percent"></a>


|  | 
| --- |
| This slot type is in preview release for Amazon Lex and is subject to change\. | 

Converts words and symbols that represent a percentage into a numeric value with a percent sign \(%\)\.

If the user enters a number without a percent sign or the word "percent," the slot value is set to the number\. The following table shows how the `AMAZON.Percentage` slot type captures percentages\.


| Input | Response | 
| --- | --- | 
| 50 percent | 50% | 
| 0\.4percent | 0\.4% | 
| 23\.5% | 23\.5% | 
| 25 | 25 | 