Check whether the given string is a subsequence of the plaintext alphabet.
Example
For s = "effg" or s = "cdce", the output should be
alphabetSubsequence(s) = false;
For s = "ace" or s = "bxz", the output should be
alphabetSubsequence(s) = true.
```java
boolean alphabetSubsequence(String s) {    
    for(int i=0; i<s.length()-1; i++){
        if(s.charAt(i)>=s.charAt(i+1)) return false;        
    }    
    return true;
}
```