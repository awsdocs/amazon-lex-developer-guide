# Built\-in Slot Types<a name="howitworks-builtins-slots"></a>

Amazon Lex supports built\-in slot types that define how data in the slot is recognized and handled\. You can create slots of these types in your intents\. This eliminates the need to create enumeration values for commonly used slot data such as date, time, and location\. Built\-in slot types do not have versions\. 


| Slot Type | Short Description | Supported Locales | 
| --- | --- | --- | 
| [AMAZON\.Airport](built-in-slot-airport.md) | Recognizes words that represent an airport\. | All locales | 
| [AMAZON\.AlphaNumeric](built-in-slot-alphanumeric.md) | Recognizes words made up of letters and numbers\. | All locales | 
| [AMAZON\.City](built-in-slot-city.md) | Recognizes words that represent a city\. | All locales except English \(US\) | 
| [AMAZON\.Country](built-in-slot-country.md) | Recognizes words that represent a country\. | All locales | 
| [AMAZON\.DATE](built-in-slot-date.md) | Recognizes words that represent a date and converts them to a standard format\. | All locales | 
| [AMAZON\.DURATION](built-in-slot-duration.md) | Recognizes words that represent duration and converts them to a standard format\. | All locales | 
| [AMAZON\.EmailAddress](built-in-slot-email.md) | Recognizes words that represent an email address and converts them into a standard email address\. | All locales | 
| [AMAZON\.FirstName](built-in-slot-first-name.md) | Recognizes words that represent a first name\. | All locales except English \(US\) | 
| [AMAZON\.LastName](built-in-slot-last-name.md) | Recognizes words that represent a last name\. | All locales except English \(US\) | 
| [AMAZON\.NUMBER](built-in-slot-number.md) | Recognizes numeric words and converts them into digits\. | All locales | 
| [AMAZON\.Percentage](built-in-slot-percent.md) | Recognizes words that represent a percentage and converts them to a number and a percent sign \(%\)\. | All locales | 
| [AMAZON\.PhoneNumber](built-in-slot-phone.md) | Recognizes words that represent a phone number and converts them into a numeric string\. | All locales | 
| [AMAZON\.SpeedUnit](built-in-slot-speed.md) | Recognizes words that represent a speed unit and converts them into a standard abbreviation\. | English \(US\) | 
| [AMAZON\.State](built-in-slot-state.md) | Recognizes words that represent a state\. | All locales except English \(US\) | 
| [AMAZON\.StreetName](built-in-slot-street-name.md) | Recognizes words that represent a street name\. | All locales except English \(US\) | 
| [AMAZON\.TIME](built-in-slot-time.md) | Recognizes words that indicate times and converts them into a time format\. | All locales | 
| [AMAZON\.WeightUnit](built-in-slot-weight.md) | Recognizes words that represent a weight unit and converts them into a standard abbreviation  | English \(US\) | 

**Note**  
For the English \(US\) \(en\-US\) locale, Amazon Lex supports slot types from the Alexa Skill Kit\. For a list of available built\-in slot types, see the [Slot Type Reference](https://developer.amazon.com/docs/custom-skills/slot-type-reference.html) in the Alexa Skills Kit documentation\.   
Amazon Lex doesn't support the `AMAZON.LITERAL` or the `AMAZON.SearchQuery` built\-in slot types\. 