##### 이 문제는 코드가 중요하기 보다는 푸는 방법이 중요하였음

```java
import java.util.*;
class Solution {
    public int solution(int[] weight) {        
        Arrays.sort(weight);
        
        int sum = 0;
        for(int i=0; i<weight.length; i++){            
            if(sum+1<weight[i]) break;            
            sum += weight[i];
        }
        
        return sum+1;
    }    
}```
