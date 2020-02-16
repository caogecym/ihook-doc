---
id: comparison
title: Comparison
---

When configuring notification conditions, you may use the following method to compare between response source value and expected value.

| Comparison | Description |
| :------- | :----- |
| equal	(string) | A string equality check on the given property and value. The check is case sensitive.|
| not equal	(string) | The given string property is not equal to the given string value. The check is case sensitive.|
| contains (string)	| The given string value is found in the given property. The check is case sensitive.|
| not contain (string) | The given string value is not found in the given property. The check is case sensitive.|
| equals (number) | The source property is numerically equal to the given value. This comparison ensures the values are able to be converted to numbers.|
| not equal	(number) | The given property is not equal to the given number value.|
| greater than (number) | The given property is greater than the given number value.|
| greater than or equal	(number) | The given property is greater than or equal to the given number value.|
| less than	(number) | The given property is less than the given number value.|
| less than or equal (number) | The given property is less than or equal to the given number value.|
| has key	| The JSON property evaluates to an object and contains the given value as a key. Source must be Response Body (JSON). The check is case sensitive.|
| has value	| The JSON property evaluates to an array and contains the given value as an element. Source must be Response Body (JSON). The check is case sensitive.|
| is null	| The JSON property has a NULL value. Source must be Response Body (JSON).|