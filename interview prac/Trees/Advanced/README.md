```java
//
// Binary trees are already defined with this interface:
// class Tree<T> {
//   Tree(T x) {
//     value = x;
//   }
//   T value;
//   Tree<T> left;
//   Tree<T> right;
// }

HashMap<Integer, Integer> map = new HashMap<>();
int[] mostFrequentSum(Tree<Integer> t) {
    if(t==null) return new int[]{};
    getSum(t);
    int max = 0;
    ArrayList<Integer> list = new ArrayList<>();
    
    Set<Integer> keySet = map.keySet();
    Iterator<Integer> iter = keySet.iterator();
    while(iter.hasNext()){
        int key = iter.next();
        int value = map.get(key);
        if(max<value){
            max = value;
            list.clear();
            list.add(key);
        }else if(max==value) list.add(key);
    }
    //if(list.size()==0) return new int[]{};
    return list.stream().sorted().mapToInt(i->i).toArray();

}

int getSum(Tree<Integer> t){
    int left = t.left!=null?getSum(t.left):0;
    int right = t.right!=null?getSum(t.right):0;
    int sum = t.value + left + right;
    if(!map.containsKey(sum)){
        map.put(sum, 1);
    }else{
        map.put(sum, map.get(sum)+1);
    }
    return sum;
    
}
```