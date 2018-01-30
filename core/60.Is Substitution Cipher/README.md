A ciphertext alphabet is obtained from the plaintext alphabet by means of rearranging some characters. For example "bacdef...xyz" will be a simple ciphertext alphabet where a and b are rearranged.
A substitution cipher is a method of encoding where each letter of the plaintext alphabet is replaced with the corresponding (i.e. having the same index) letter of some ciphertext alphabet.
Given two strings, check whether it is possible to obtain them from each other using some (possibly, different) substitution ciphers.
Example
For string1 = "aacb" and string2 = "aabc", the output should be
isSubstitutionCipher(string1, string2) = true.
Any ciphertext alphabet that starts with acb... would make this transformation possible.
For string1 = "aa" and string2 = "bc", the output should be
isSubstitutionCipher(string1, string2) = false.

##### 내 풀이가 가장 좋은 듯... 거의 Hashmap을 썼음

```java
boolean isSubstitutionCipher(String string1, String string2) {
    int[] a = new int[26];
    int[] b = new int[26];    
    for(int i=0; i<string1.length(); i++){
        int m = a[string1.charAt(i)-97]++;
        int n = b[string2.charAt(i)-97]++;        
        if(m!=n){
            return false;
        }
    }
    return true; 
}
```

##### Hashmap을 쓴 풀이
```java
boolean isSubstitutionCipher(String string1, String string2) {
    int length = string1.length();
    
    Map<Character, Character> replacementMap = new HashMap<>();
    
    for (int i = 0; i < length; i++) {
        Character char1 = string1.charAt(i);
        Character char2 = string2.charAt(i);
        
        if (replacementMap.containsKey(char1)) {
            Character previousChar2 = replacementMap.get(char1);
            if (!char2.equals(previousChar2)) {
                return false;
            }
        } else {
            replacementMap.put(char1, char2);
        }
    }
    
    return replacementMap.size() == new HashSet<>(replacementMap.values()).size();
}
```