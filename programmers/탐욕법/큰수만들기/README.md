
```java
import java.util.*;
class Solution {
    public String solution(String number, int k) {
        String answer = "";
        
        Stack<Character> stack = new Stack<>();
        
        for(int i=0; i<number.length(); i++){
            if(stack.size()==0 || k==0){
                stack.add(number.charAt(i));
            }else{
                while(stack.size()>0 && k>0){
                    if(stack.peek()<number.charAt(i)){
                        stack.pop();
                        k--;
                    }else{
                        break;
                    }
                }
                stack.add(number.charAt(i));
            }
        }
        StringBuilder builder = new StringBuilder();
        while(stack.size()>0){
            builder.insert(0, stack.pop());
        }
        
        
        
        return builder.substring(0, builder.length()-k);
    }
}
```