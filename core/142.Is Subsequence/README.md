Given a string s, determine if it is a subsequence of a given string t.

Example

For t = "CodeSignal" and s = "CoSi", the output should be
isSubsequence(t, s) = true;

For t = "CodeSignal" and s = "cosi", the output should be
the output should be
isSubsequence(t, s) = false.

[input] string t

A string consisting of English letters, whitespace characters (' '), digits and punctuation marks (".,?!=*+-").

Guaranteed constraints:
0 ≤ t.length ≤ 500.

[input] string s

A string consisting of English letters, whitespace characters (' '), digits and punctuation marks (".,?!=*+-").

```java
boolean isSubsequence(String t, String s) {
  String pattern = "";
  for (int i = 0; i < s.length(); i++) {
    pattern += ".*[" + s.charAt(i) + "]" ;
  }
  Pattern regex = Pattern.compile(pattern);
  return regex.matcher(t).find();
}
```