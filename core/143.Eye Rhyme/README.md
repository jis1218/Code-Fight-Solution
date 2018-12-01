An eye rhyme is a rhyme in which two words are spelled similarly but pronounced differently. An example is the pair cough and bough; although they look similar, when they are spoken there is no rhyming quality.

You are writing a thesis on the eye rhyme, and you thought it would be cool to make the text itself eye rhymed. This brilliant idea came to your mind a little too late: the text is already written. Now you want to check if a given pair of lines in your text have an eye rhyme. More specifically, you want to make sure that the last three characters of each pair of lines coincide.

You have already split your text into pairs of lines. Now all that's left is to check that the last three characters of the lines in each pairOfLines coincide. Implement a function that will do this job.

Example

For pairOfLines = "cough\tbough", the output should be
eyeRhyme(pairOfLines) = true.

```java
Boolean eyeRhyme(String pairOfLines) {
  Pattern pattern = Pattern.compile(".*(.{3})\\t.*(.{3})");
  Matcher matcher = pattern.matcher(pairOfLines);
  matcher.matches();
  return matcher.group(1).equals(matcher.group(2));
}
```