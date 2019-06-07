```java
int[] citiesConquering(int n, int[][] roads) {
    HashMap<Integer, ArrayList<Integer>> map = new HashMap<>();
    int[] result = new int[n];
    Arrays.fill(result, 1);
    for(int i=0; i<roads.length; i++){
        ArrayList<Integer> list = map.getOrDefault(roads[i][0], new ArrayList<Integer>());
        list.add(roads[i][1]);
        map.put(roads[i][0], list);
        
        ArrayList<Integer> list2 = map.getOrDefault(roads[i][1], new ArrayList<Integer>());
        list2.add(roads[i][0]);
        map.put(roads[i][1], list2);        
    }
    int count = 1;
    while(true){
        boolean flag = true;
        ArrayList<Integer> index = new ArrayList<>();
        for(int i=0; i<n; i++){
            if(!map.containsKey(i)) continue;
            
            if(map.get(i).size()==1){                
                index.add(i);  
            }            
        }
        for(int i : index){
            if(map.get(i).size()>0){
                int temp = map.get(i).get(0);
                map.get(temp).remove(Integer.valueOf(i));
            }            
            map.remove(i);
            flag = false;
            result[i] = count;
        }
        System.out.println(flag);
        count++;
        if(flag){
            for(int j : map.keySet()){
                result[j] = -1;
            }
            break;
            
        } 
    }
    return result;

}

```