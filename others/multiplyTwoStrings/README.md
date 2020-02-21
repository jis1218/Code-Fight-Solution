Avoid using built-in big integers when solving this challenge. Implement them yourself, since this is what you would be asked to do during a real interview.

Multiply two numbers that have been given to you as strings, s1 and s2, and return the result as a string. Neither s1 nor s2 contain leading zeros, and your answer shouldn't either.

Example

For s1 = "15" and s2 = "3", the output should be
multiplyTwoStrings(s1, s2) = "45";
For s1 = "13" and s2 = "13", the output should be
multiplyTwoStrings(s1, s2) = "169".
```java
String multiplyTwoStrings(String s1, String s2) {
    int stor[] = new int[10000000];
    int s1len = s1.length();
    int s2len = s2.length();
    for(int i=0; i<s1len; i++){
        int num = s1.charAt(i)-'0';
        for(int j=0; j<s2len; j++){
            stor[s2len+s1len-i-j-2] += num*(s2.charAt(j)-'0');
        }
    }
    StringBuilder builder = new StringBuilder();
    int prev = 0;
    for(int i=0; i<s1len+s2len-1; i++){
        stor[i]+=prev;
        builder.append(stor[i]%10);        
        prev = stor[i]/10;
    }
    if(prev!=0) builder.append(prev);
    return builder.reverse().toString();
}
```