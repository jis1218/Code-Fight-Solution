##### 너무 어렵게 생각하지 말자!
```java
import java.lang.*;

class Solution
{
    public int solution(String s)
    {
        int max = 1;
        for(int i=0; i<s.length(); i++){
            int count = 1;
            int count2 = 0;
            for(int j=1; i-j>=0 && i+j<s.length();j++){                
                if(s.charAt(i+j)==s.charAt(i-j)){
                    count+=2;                        
                }else break;                              
            }
            if(count>max) max = count;
            
            for(int j=0; i-j-1>=0 && i+j<s.length(); j++){
                if(s.charAt(i+j)==s.charAt(i-j-1)){
                    count2+=2;                        
                }else break; 
            }
            if(count2>max) max = count2;
        }
        return max;
    }
}
```