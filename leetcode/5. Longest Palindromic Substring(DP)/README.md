##### DP 이용한 풀이
```java
class Solution {
    int max = 0;
    int storage[] = new int[2];
    public String longestPalindrome(String s) {
        for(int i=0; i<s.length(); i++){
            if(i+1<s.length() && s.charAt(i)==s.charAt(i+1)){
                checkPalindrome(i, i+1, s, 2);
            }
            checkPalindrome(i, i, s, 1);   
            
        }
        
        return s.substring(storage[0], storage[1]+1);
    }
    
    public void checkPalindrome(int prev, int next, String s, int len){
        
        if(max<len){
            max = len;
            storage[0] = prev;
            storage[1] = next;
        } 
        if(prev-1<0 || next+1>s.length()-1) return;
        if(s.charAt(prev-1)==s.charAt(next+1)){
            checkPalindrome(prev-1, next+1, s, len+2);
        }
        return;
    }
}
```