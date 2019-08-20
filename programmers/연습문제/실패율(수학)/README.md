```java
import java.util.*;
import java.util.stream.*;
class Solution {
    public int[] solution(int N, int[] stages) {
        int[] answer = {};
        int[] reach = new int[N];
        Double[] fail = new Double[N];
        Arrays.fill(fail, 0.0d);        
        for(int i=0; i<stages.length; i++){
            if(stages[i]-1!=N){
                reach[stages[i]-1]++;
            }
            
        }
        int total = stages.length;
        for(int i=0; i<fail.length; i++){
            fail[i] = Double.valueOf((double)reach[i]/total);           
            
            System.out.println(fail[i]);
            total -= reach[i];        
            if(total==0) break;
        }
        
        int sortedIndices[] = IntStream.range(0, N).boxed().sorted((i,j) ->
        fail[j].compareTo(fail[i])).mapToInt(e->e+1).toArray();
        for(int i : sortedIndices){
            System.out.println(i);
        }
        
        return sortedIndices;
    }
}
```