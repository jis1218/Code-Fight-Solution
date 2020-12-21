```java
class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        Map<Integer, Integer> map = new LinkedHashMap<>();
        
        for(int i : nums){
            int cnt = map.getOrDefault(i, 0);
            map.put(i, ++cnt);
        }
        
        List<Map.Entry<Integer, Integer>> entries = new LinkedList<>(map.entrySet());
        Collections.sort(entries, (o1, o2) -> o2.getValue().compareTo(o1.getValue()));
        int[] answer = new int[k];
        int count = 0;
        for(Map.Entry<Integer, Integer> entry : entries){
            answer[count++] = entry.getKey();
            if(count>=k) break;
        }
        return answer;
    }
}
```