You are given two strings s and t of the same length, consisting of uppercase English letters. Your task is to find the minimum number of "replacement operations" needed to get some anagram of the string t from the string s. A replacement operation is performed by picking exactly one character from the string s and replacing it by some other character.
Example
For s = "AABAA" and t = "BBAAA", the output should be
createAnagram(s, t) = 1;
For s = "OVGHK" and t = "RPGUC", the output should be
createAnagram(s, t) = 4.

```java
int createAnagram(String s, String t) {    
    int[] a = new int[26];
    int[] b = new int[26];
    
    for(int i=0; i<s.length(); i++){
        a[s.charAt(i)-'A']++;
    }
    for(int j=0; j<t.length(); j++){
        b[t.charAt(j)-'A']++;
    }    
    int sum=0;    
    for(int m=0; m<26; m++){
        if(a[m]!=0 && b[m]!=0)
        sum += Math.min(a[m], b[m]);
    }    
    return s.length()-sum;
}
```

##### getBytes를 이용한 풀이도 있음, 결론적으로는 위의 풀이와 비슷
##### getBytes를 하면 ASCII 코드의 값을 얻을 수 있음

```java
int createAnagram(String s, String t) {
    int[] count = new int[256];
    for (byte b : s.getBytes())
        count[b]++;
    for (byte b : t.getBytes())
        count[b]--;
    int total = 0;
    for (int i : count)
        if (i > 0)
            total += i;
    return total;
}
```