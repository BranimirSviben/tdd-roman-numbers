# TDD-roman-numbers

Roman/Arabic numbers conversion application built with TDD

<br>
---

## The Problem
---
In order to convert arabic numbers to roman and vice versa, we need to understand the problems and complexities of the conversions and develop appropriate algorithms to solve them.

### Arabic -> Roman algorithm/pseudocode

- accept an arabic number as a parameter for conversion
- check if arabic number is of correct type (integer, short, long)
- check if it is in valid range [0 - 3999]
- check which is the highest roman numeral that can be used to describe the number, ex. 3456 -> M, 286 -> C, 6 -> V, ...
- recursively loop backwards through the roman numerals list (from their higher to lower integer values), starting from the numeral found in previous step until you reach the numeral "I"
    - check if integer value of the current numeral is power of 10
        - if it is power of 10, find its multiplier in the number under conversion (ex. 3456/1000 = 3) and write the numeral down that many times, ex. "MMM"
        - else, for V, L and D numerals we determine if the value of the number is lower than the value of the numeral
            - if it is we prepend it with the approppriate number of the first preceeding power of 10 numeral, ex. for the value V, we write IV... preceeding numeral I (power of 10) written one time before V
            - else we just write down the numeral, ex. 56 is larger than 50 (L) so we write L 
    - subtract from the number under conversion the integer value of the numerals we already writen down and continue with the loop

The method that implements the above described algorithm should recursively call itself, each time passing the value of the number that has been subtracted in the previous recursion as its parameter. 

When all recursions are done, it should return the correctly written roman number.


### System design
---

After the apparently working and correct pseudocode is written, we can start planning the design of the system and its components.

- **RomanNumerals** class - Contains a static list of roman numerals (list of elements of type "RomanNumeral")

- **RomanNumeral** class 
    - Inner class of **RomanNumerals** with **romanNumeral** property and it's corresponding **arabicNumeral** property (1, I), ...
    - Overriden getter method that returns the mapped numeral based on the numeral passed in as a parameter, ex. (String numeral) -> RomanNumeral romanNumeral
    - Method that return the number with the highest integer value that can be written using only the roman numeral that is passed in as a parameter, and those lower in value than him, ex. (I) -> 3, (V) -> 6, (X) -> 39, (L) -> 89, ... 
    - Method that checks whether the integer value of a roman numeral passed in as a parameter, is a power of 10, ex. (I) -> true, (V) -> false, (X) -> true, ...

- **Converter** interface - Interface that exposes APIs for two way numbers conversion... it's implementations implement the appropriate conversion algorithms (Arabic to Roman and vice versa)


<br>

---
<br>

## tdd hints

-   test interfaces (behaviour), not implementations