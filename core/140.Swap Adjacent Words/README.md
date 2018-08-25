You are given a string consisting of words separated by whitespace characters, where the words consist only of English letters. Your task is to swap pairs of consecutive words and return the result.
Example
For s = "CodeFight On", the output should be
swapAdjacentWords(s) = "On CodeFight";
For s = "How are you today guys", the output should be
swapAdjacentWords(s) = "are How today you guys".

```java
String swapAdjacentWords(String s) {
  return s.replaceAll("(\\b\\w+\\b)\\s+(\\b\\w+\\b)", "$2 $1");
}
```

##### (\b\w+\b) capture first word
##### \s+ which is followed by a space or more
##### (\b\w+\b) capture second word