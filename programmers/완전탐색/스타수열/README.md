```java
import java.util.*;
class Solution {
    public int solution(int[] a) {
        int answer = -1;
        int store[] = new int[a.length];
        HashSet<Integer> set = new HashSet<>();
        for(int i : a){
            store[i]++;
            set.add(i);
        }
        
        Iterator<Integer> iter = set.iterator();
        int max = 0;
        
        while(iter.hasNext()){
            int count = 0;
            int temp = iter.next();            
            if(max>store[temp]) continue;
            for(int i=0; i<a.length; i++){
                if(i+1<a.length && 
                   ((a[i]==temp && a[i+1]!=temp) 
                    || (a[i]!=temp && a[i+1]==temp))){
                    count++;
                    i++;
                }
            }
            //System.out.println(count);
            if(max<count) max = count;
        }
        return max*2;
    }
}
```