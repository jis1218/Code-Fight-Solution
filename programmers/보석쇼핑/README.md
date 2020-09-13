```java
import java.util.*;
class Solution {
    public int[] solution(String[] gems) {
        int[] answer = {};

        HashSet<String> set = new HashSet<>(Arrays.asList(gems));
        //System.out.println(set.size());
        int size = set.size();

        HashMap<String, Integer> map = new HashMap<>();
        TreeSet<Integer> treeSet = new TreeSet<>();

        int min=0, max=0, lenMin = gems.length;
        int realMin = 0, realMax = 0;

        for(int i=0; i<gems.length; i++){
            if(map.containsKey(gems[i])){
                treeSet.remove(map.get(gems[i]));
            }
            map.put(gems[i], i);
            treeSet.add(i);
            if(isMapFull(size, map)){
                max = treeSet.last();
                min = treeSet.first();
                //System.out.println("min = " + min + ", max = " + max);
                if(lenMin>max-min){
                    lenMin = max-min;
                    realMin = min;
                    realMax = max;
                }
            }

        }
        return new int[] {realMin+1, realMax+1};
    }

    public boolean isMapFull(int size, HashMap<String, Integer> map){
        return size==map.size();
    }
}
```

```java
import java.util.*;
class Solution {
    public int[] solution(String[] gems) {
        int[] answer = {};
        HashSet<String> set = new HashSet<>();
        HashMap<String, Integer> map = new HashMap<>();

        for(String s : gems){
            set.add(s);
        }
        int size = set.size();
        int minIdx = 0, maxIdx = 0;
        int idx = 0;
        int minLength = gems.length;
        while(idx<=gems.length){
            //System.out.print(idx + ", ");

            if(map.size()!=size){
                if(idx==gems.length) break;
                String t = gems[idx];
                map.put(t, map.getOrDefault(t, 0) + 1);
                if(map.size()==size){                    
                    if(minLength>idx-minIdx){
                        maxIdx = idx;
                        minLength = idx-minIdx;
                    }
                }
                idx++;
            }else{
                String minT = gems[minIdx];
                map.put(minT, map.get(minT)-1);
                //System.out.println("minT = " + map.get(minT));
                if(map.get(minT)==0) map.remove(minT);
                else{
                    if(minLength>idx-minIdx){                        
                        minLength = idx-minIdx;
                    }
                     minIdx++;
                }
               
            }                    
        }
        //System.out.print("===" + minIdx + ", " + maxIdx);
        

        return answer;
    }
}
```