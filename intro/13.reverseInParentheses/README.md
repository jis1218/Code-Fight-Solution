Write a function that reverses characters in (possibly nested) parentheses in the input string.

Input strings will always be well-formed with matching ()s.

Example

For inputString = "(bar)", the output should be
reverseInParentheses(inputString) = "rab";
For inputString = "foo(bar)baz", the output should be
reverseInParentheses(inputString) = "foorabbaz";
For inputString = "foo(bar)baz(blim)", the output should be
reverseInParentheses(inputString) = "foorabbazmilb";
For inputString = "foo(bar(baz))blim", the output should be
reverseInParentheses(inputString) = "foobazrabblim".
Because "foo(bar(baz))blim" becomes "foo(barzab)blim" and then "foobazrabblim".

```java
String reverseInParentheses(String inputString) {
    
    int findex = inputString.lastIndexOf('(');
    int bindex = inputString.indexOf(')', findex);

    if(findex==-1 && bindex==-1) return inputString;	

    String frontStr = inputString.substring(0, findex);
    String result = inputString.substring(findex+1, bindex);
    StringBuilder builder = new StringBuilder(result);
    builder.reverse();
    result = builder.toString();
    String backStr = inputString.substring(bindex+1);

    return reverseInParentheses(frontStr + result + backStr);
}
```