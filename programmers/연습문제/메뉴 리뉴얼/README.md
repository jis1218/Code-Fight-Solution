```java
import java.util.*;
import java.util.stream.Collectors;

class Solution {
    Map<String, Integer> map = new HashMap<>();
    
    public String[] solution(String[] orders, int[] course) {
        ArrayList<String> list = new ArrayList<>();
        
        String result = "";
        for(int i=0; i<orders.length; i++) {
            for(int j=0; j<orders[i].length(); j++) {
                char[] array = orders[i].toCharArray();
                Arrays.sort(array);

                String str = String.valueOf(array);
                makeCombination(str, j, result);
            }            
        }
        
        for(int i : course) {
            HashMap<String, Integer> tempMap = new HashMap<>();
            map.forEach((key, value) -> {
                if(key.length()==i && value > 1) {
                    tempMap.put(key, value);
                }
            });
            list.addAll(
                tempMap.keySet().stream().filter(key -> tempMap.get(key) == Collections.max(tempMap.values()))
                .collect(Collectors.toList()));
        }
        
        Collections.sort(list);
        
        return list.toArray(new String[]{});
    }
    
    private void makeCombination(String order, int index, String result) {
        result = result.concat(String.valueOf(order.charAt(index)));
        
        if(result.length()>1) {
            int count = map.getOrDefault(result, 0);
            map.put(result, count+1);
            //System.out.println(result);
        }
        
        for(int i = index+1; i<order.length(); i++) {
            makeCombination(order, i, result);
            result = result.substring(0, result.length());
        }
    }
}
```

```java
import java.util.*;
import java.util.stream.*;
class Solution {
    public String[] solution(String[] orders, int[] course) {
        //String answer[] = {"", ""};

        List<String> answer = new ArrayList<>();
        for(int i : course){
            HashMap<String, Integer> map = new HashMap<>();
            helper(orders, i, map);
            List<String> list = map.entrySet()
                .stream()
                .filter(entry -> entry.getValue()>1 &&  entry.getValue()==Collections.max(map.values()))
                .map(Map.Entry::getKey)
                .collect(Collectors.toList());

            answer.addAll(list);
        }
        //answer.stream().forEach(System.out::println);
        return answer.stream().sorted().toArray(String[]::new);
    }

    public void helper(String[] orders, int len, HashMap<String, Integer> map){
        for(String s : orders){            
            combi(s, 0, len, map, "");            
            //break;
        }
    }

    public void combi(String s, int idx, int len, HashMap<String, Integer> map, String word){
        if(word.length()==len){
            char[] chars = word.toCharArray();
            Arrays.sort(chars);
            word = new String(chars);
            int count = map.getOrDefault(word, 0)+1;
            //System.out.println(word + ", " + count);
            map.put(word, count);
            return;
        }

        for(int i=idx; i<s.length(); i++){
            word += s.charAt(i);
            //System.out.print("i = " + i + ", ");
            combi(s, i+1, len, map, word);
            //System.out.println(word);
            if(word.length()!=0) word = word.substring(0, word.length()-1);
            //System.out.println("sub = " + word);
        }
        //if(word.length()!=0) word = word.substring(0, word.length()-1);
    }
}
```