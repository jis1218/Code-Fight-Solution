You're given a substring s of some cyclic string. What's the length of the smallest possible string that can be concatenated to itself many times to obtain this cyclic string?
Example
For s = "cabca", the output should be
cyclicString(s) = 3.
"cabca" is a substring of a cycle string "abcabcabcabc..." that can be obtained by concatenating "abc" to itself. Thus, the answer is 3.
```java
int cyclicString(String s) {
    
    for(int i=1; i<=s.length(); i++){
        boolean flag = true;
        for(int j=i; j<s.length(); j = i+j){
            int max = i+j>s.length()?s.length():i+j;
            System.out.println(s.substring(0,i) + ", " + s.substring(j, max));
            if(!s.substring(0,s.substring(j,max).length()).contains(s.substring(j, max))){
                flag = false;
                break;
            }
        }
        if(flag) return i;        
    }
    return s.length();
}
```

##### 다른 풀이
```java
int cyclicString(String s) {
    for (int i = s.length(); i-- > 0;) {
        String t = s.substring(i);
        String sum = "";
        while (sum.length() < s.length())
            sum = t + sum;
        if (sum.endsWith(s))
            return t.length();
    }
    return -1;
}
```