# AMAZON\.Percentage<a name="built-in-slot-percent"></a>

Converts words and symbols that represent a percentage into a numeric value with a percent sign \(%\)\.

If the user enters a number without a percent sign or the word "percent," the slot value is set to the number\. The following table shows how the `AMAZON.Percentage` slot type captures percentages\.


| Input | Response | 
| --- | --- | 
| 50 percent | 50% | 
| 0\.4 percent | 0\.4% | 
| 23\.5% | 23\.5% | 
| twenty five percent | 25% | 