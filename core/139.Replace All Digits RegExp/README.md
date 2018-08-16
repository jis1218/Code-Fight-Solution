Implement the missing code, denoted by ellipses. You may not modify the pre-existing code.
Implement a function that replaces each digit in the given string with a '#' character.
Example
For input = "There are 12 points", the output should be
replaceAllDigitsRegExp(input) = "There are ## points".

```java
String replaceAllDigitsRegExp(String input) {
  return  input.replaceAll("[0-9]", "#") ;
}```
