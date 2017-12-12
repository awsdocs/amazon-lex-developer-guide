# AMAZON\.NUMBER<a name="built-in-slot-number"></a>


|  | 
| --- |
| This slot type is in preview release for Amazon Lex and is subject to change\. | 

Converts numeric words into digits\.

Amazon Lex extends the [AMAZON\.NUMBER](https://developer.amazon.com/public/solutions/alexa/alexa-skills-kit/docs/built-in-intent-ref/slot-type-reference#number) slot type to convert words or numbers that express a number into digits, including decimal numbers\. The following table shows how the `AMAZON.NUMBER` slot type captures numeric words\.


| Input | Response | 
| --- | --- | 
| one hundred twenty three point four five | 123\.45 | 
| one hundred twenty three dot four five | 123\.45 | 
| point four two | 0\.42 | 
| point forty two | 0\.42 | 
| 232\.998 | 232\.998 | 
| 50 | 50 | 