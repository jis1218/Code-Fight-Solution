```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        HashMap<Character, Integer> map = new HashMap<>();
        int max = 0;
        int min = -1;
        int len = 0;
        for(int i=0; i<s.length(); i++){
            char c = s.charAt(i);
            if(map.containsKey(c)){
                if(min<map.get(c)) min = map.get(c);
            }
            len=i-min;
            map.put(c, i);
            if(len>max) max=len;
        }
        return max;
    }
}
```