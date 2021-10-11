Given a string s which consists of lowercase or uppercase letters, return the length of the longest palindrome that can be built with those letters.

Letters are case sensitive, for example, "Aa" is not considered a palindrome here.
```java
class Solution {
    public int longestPalindrome(String s) {
        int alphabet[] = new int['z' - 'A' + 1];
        
        for(int i=0; i<s.length(); i++) {
            alphabet[s.charAt(i)-'A']++;
        }
        int sum = 0;
        boolean isOddExist = false;
        for(int i : alphabet) {
            sum += i/2;
            if(!isOddExist && i%2==1) isOddExist = true;
        }
        
        return sum * 2 + (isOddExist?1:0);
    }
}
```

##### 나누기를 하면 시간이 걸리기 때문에 다음과 같은 풀이도 있음
```java
class Solution {
    public int longestPalindrome(String s) {
        int[] count = new int[128];
        int length = 0;
        for(char c: s.toCharArray()){
            if(++count[c] == 2){
                length += 2;
                count[c] = 0;
            }
        }
        //만약 모든 알파벳이 2개씩 있다면 palindrome의 길이는 s의 길이와 같을 것이므로...
        return (length == s.length())? length: length+1;
    }
}
```