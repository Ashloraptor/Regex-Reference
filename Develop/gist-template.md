# Regex Reference

Regex, or regular expression, is a tool that can be utilized in many cases to search for string patterns, and in some instances manipulate, replace, or capture our finds. This capability is commonly utilized in searching usernames, masking phone numbers or emails, or formatting for typography.

## Summary

In this tutorial, we will use password formatting as an example, though regex can be used for many other applications.
When making a password, there is a variety of criteria that may be required. In this instance, we’ll permit/require
    • minimum 6 characters
    • maximum 16 characters
    • lowercase letters between a and z
    • capital letters between a and z
    • numbers
    • some special characters
Our regex will appear as the following:
```
/^[a-zA-Z0-9!@#$%^&*()_-]{6,16}$/
```

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [Character Classes](#character-classes)
- [Flags](#flags)
- [Grouping and Capturing](#grouping-and-capturing)
- [Bracket Expressions](#bracket-expressions)
- [Greedy and Lazy Match](#greedy-and-lazy-match)
- [Boundaries](#boundaries)
- [Back-references](#back-references)
- [Look-ahead and Look-behind](#look-ahead-and-look-behind)

## Regex Components

Regex can utilize literal characters- characters which mean exactly what they mean, such as the lowercase letter a being a lowercase letter a. Regex can also utilize meta characters, in which the character used is a representation of another meaning.
Referencing our example regex, the ```/``` at the beginning and end of the string are not literally the slash character. The combination ```/^``` marks the beginning of the string, while ```$/``` marks the end of the string. The square brackets ```[]``` denote a range of optional acceptable input within. 

### Anchors

An example of a meta character is ```^```, or caret. When used as an anchor, ```^``` works in conjunction with following characters to signify the beginning of a string. For example, you might use ```^T``` when searching to find a string that begins with a capital T, pulling up examples with The or Therefore.
Alternatively, ```$``` can be used as an anchor to signify the end of a string. ```$``` can be used in conjunction with preceding characters to locate the ends of strings which match the requisite. An example can include ```s$``` for any string that ends with a lowercase s.

### Quantifiers

Quantifiers allow us to specify the length of a string. For instance, we may want to limit a phone number to 10 digits, or in our case, the length of a password. Specifically, it means to match that many of the preceding tokens. Quantifiers often include a minimum and maximum range, separated out by a comma. In our example, we want a minimum of 6 characters, and a maximum of 16, and we have distinguished the quantifier by wrapping it in ```{}```.
There are other ways to set limits to the string you’re trying to match with your regex:
* ```*``` matches the pattern 0 or more times
* ```+``` matches one or more times
* ```?``` matches either zero or one time

Curly brackets can also be used in different ways outside of requiring a minimum and maximum range. Having one number in brackets will match the pattern only as many times as specified by the value of the number. Placing a comma after the number will turn that value into the minimum.

### Character Classes

Characters are characterized by various classes. These indicators we use for classes are case sensitive.
* ```\d``` represents any numerical digit between 0 and 9
* ```.*``` represents a wild card, or any character
* ```\w``` represents any alphanumerical character, so anything uppercase or lowercase from a-z and any number from 0-9.
* ```\s``` represents any white space
* ```.``` matches any character
* ```\W``` represents anything that is not a word character, so the inverse of \w.
* ```\S``` is also inverse, representing anything that is not a space.

### Flags

Flags are placed at the end of the regex, so after the second slash to specify additional qualities for the regex.
* ```i``` allows you to ignore the case of letters when attempting to match.
* ```g``` allows all possible matches by searching globally
* ```m``` allows multi-line searching.
Less frequently used flags include: 
* ```s``` allows single line (dotall)
* ```u``` allows unicode search
* ```y``` allows sticky search

### Grouping and Capturing

Grouping allows for us to manipulate our data. By default, the entirety of a string is indicated as Group 0. We may in the future want to mask only part of our data, for instance with protecting phone numbers, where we allow the area code to remain visible, but hide the actual numbers, for example (210)XXX-XXXX. Or, we may want to allow our users to confirm submissions, and may mask all but the last four digits of a Social Security number, or all but the domain of an email. To partially manipulate these strings, we’ll identify additional groups and what we want to replace them with to present to the user.
When doing so, we use a set of parenthesis to create a subexpression. Phone numbers are easy to use in demonstration of this. We may have phone numbers in the format of ###-###-####. (###-###-####) puts the entire group into a set of parenthesis to represent group 0. If we format it as ((###)-(###)-(####)), the area code will be group 1, the three digits in the middle will be group 2, and the last four digits are group 3. If trying to match a phone number with a regex, our regex may look like ```\d{3}-\d{3}-\d{4}```, but when specifying the group, it could look more like ```\d{3}-\d{3}-(\d{4})```.

### Bracket Expressions

Bracket expressions allow us to shorthand which characters we want to include. When used between characters within brackets, the hyphen will refer to the range of characters between, rather than the literal hyphen. This is why we are able to specify ```[a-z]``` for all lowercase letters or ```[A-Z]``` for all uppercase letters, rather than typing out each individually acceptable letter.

### Greedy and Lazy Match

By default, quantifiers are greedy. This means that in a search, they will match as many occurrences as possible.
Lazy mode will instead repeat a minimal number of times. Though we referenced ```?``` earlier as being a quantifier for either zero or one, its meaning changes when used after another quantifier (including itself), turning on lazy mode.

### Boundaries

Boundaries can be indicated with ```\b``` to represent the beginning or end of a word or series of characters in a string. Without them, searching within the regex can refer to a series of characters that refer to parts of a word, and skew the results we may desire. Being able to specify the boundary is the difference between color and coloring, or house and houses, different and indifferent.

### Back-references

Backreference refers to the submatch of a previous capturing group. To backreference the captured group, we will use ```$``` and the number or ```\``` and the number to refer to the number of the group, using ```$``` for replacing the characters outside of the group or ```\``` to refer to the string.

### Look-ahead and Look-behind

Look-ahead allows us to incorporate additional patterns when searching one out. By including ```(?=y)``` after ```x```, we can find any matches of ```x``` in which y follows it, but only such instance of ```x``` will be matched. Look-behind behaves inversely. When looking for a match, we would place a condition to precede the match we seek, using ```(?<=y)x``` to find the ```x```.

## Author

This tutorial is written by [Ashloraptor](https://github.com/Ashloraptor). 

Sources:

[RexEgg](https://www.rexegg.com/regex-anchors.html)

[The Coding Train](https://www.youtube.com/watch?v=7DG3kCDx53c)

[GitHub Regex-Tutorial](https://coding-boot-camp.github.io/full-stack/computer-science/regex-tutorial)

[RegExr](https://regexr.com/)

[JAVASCRIPT.INFO](https://javascript.info/regexp-greedy-and-lazy)
