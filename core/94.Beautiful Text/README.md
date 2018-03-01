Consider a string containing only letters and whitespaces. It is allowed to replace some (possibly, none) whitespaces with newline symbols to obtain a multiline text. Call a multiline text beautiful if and only if each of its lines (i.e. substrings delimited by a newline character) contains an equal number of characters (only letters and whitespaces should be taken into account when counting the total while newline characters shouldn't). Call the length of the line the text width.
Given a string and some integers l and r (l ≤ r), check if it's possible to obtain a beautiful text from the string with a text width that's within the range [l, r].
```java
boolean beautifulText(String inputString, int l, int r) {
    int len = inputString.length();
    boolean flag = false;
    
    for(int i=l; i<=r; i++){
        int line = (len+1)/(i+1);   
        
        if(inputString.length()==line*(i+1)-1){            
            System.out.println(i);
            flag = true;
            for(int k=1; k<line; k++){
                if(inputString.charAt(k*i+k-1)!=32){                    
                    flag = false;
                    break;
                }
            }
            if(flag) break;
        }        
    }    
    return flag;
}
```
##### 이런 요상한 풀이도 있음
```java
boolean beautifulText(String s, int l, int r) {
        return IntStream.rangeClosed(l, r).anyMatch(i -> s.matches(String.format("(.{%s} )+.{%s}", i, i)));
    }
```

##### 내 풀이와 비슷하나 좀 더 괜찮은 풀이
```java
boolean beautifulText(String inputString, int l, int r) {
    for (int i = l; i <= r; i++) {
        if ((inputString.length()+1)%(i+1) == 0) {
            boolean can = true;
            for (int j = i; j < inputString.length(); j+= i+1)
                if (inputString.charAt(j) != ' ')
                    can = false;
            if (can)
                return true;
        }
    }
    return false;
}
```