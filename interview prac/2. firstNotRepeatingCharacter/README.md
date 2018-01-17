Note: Write a solution that only iterates over the string once and uses O(1) additional memory, since this is what you would be asked to do during a real interview.
Given a string s, find and return the first instance of a non-repeating character in it. If there is no such character, return '_'.

Example
For s = "abacabad", the output should be
firstNotRepeatingCharacter(s) = 'c'.
There are 2 non-repeating characters in the string: 'c' and 'd'. Return c since it appears in the string first.
For s = "abacabaabacaba", the output should be
firstNotRepeatingCharacter(s) = '_'.
There are no characters in this string that do not repeat.

```java
char firstNotRepeatingCharacter(String s) {    
    int[] array = new int[26];    
    for(int i=0; i<s.length(); i++){        
        array[(int) s.charAt(i) -'a']++;        
    }    
    int index = s.length();    
    for(int j=0; j<26; j++){
        if(array[j]==1){
            if(index>s.indexOf(j+'a'))
            index = s.indexOf(j+'a');
        }        
    }    
    return index==s.length()?'_':s.charAt(index);    
}
```

##### 고수의 풀이
```java
char firstNotRepeatingCharacter(String s) {
    char[] c=s.toCharArray();
for(int i=0;i<s.length();i++){
    if(s.indexOf(c[i])==s.lastIndexOf(c[i]))
        return c[i];
}
    return '_';
}
```

##### 또 다른 고수의 풀이
```java
char firstNotRepeatingCharacter(String s) {
    int[] counter = new int[26];
    
    for (char c : s.toCharArray()) counter[c - 'a']++;
    
    for (char c : s.toCharArray()) {
        if (counter[c - 'a'] == 1) return c;
    }
    
    return '_';
}
```