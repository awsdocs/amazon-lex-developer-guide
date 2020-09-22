# AMAZON\.DURATION<a name="built-in-slot-duration"></a>

Converts words that indicate durations into a numeric duration\.

The duration is resolved to a format based on the [ISO\-8601 duration format](https://en.wikipedia.org/wiki/ISO_8601#Durations), `PnYnMnWnDTnHnMnS`\. The `P` indicates that this is a duration, the `n` is a numeric value, and the capital letter following the `n` is the specific date or time element\. For example, `P3D` means 3 days\. A `T` is used to indicate that the remaining values represent time elements rather than date elements\.

Examples:
+ "ten minutes": `PT10M`
+ "five hours": `PT5H`
+ "three days": `P3D`
+ "forty five seconds": `PT45S`
+ "eight weeks": `P8W`
+ "seven years": `P7Y`
+ "five hours ten minutes": `PT5H10M`
+ "two years three hours ten minutes": `P2YT3H10M`