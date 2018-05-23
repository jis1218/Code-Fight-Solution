You have a binary tree t. Your task is to find the largest value in each row of this tree. In a tree, a row is a set of nodes that have equal depth. For example, a row with depth 0 is a tree root, a row with depth 1 is composed of the root's children, etc.
Return an array in which the first element is the largest value in the row with depth 0, the second element is the largest value in the row with depth 1, the third element is the largest element in the row with depth 2, etc.
Example
For
t = {
    "value": -1,
    "left": {
        "value": 5,
        "left": null,
        "right": null
    },
    "right": {
        "value": 7,
        "left": null,
        "right": {
            "value": 1,
            "left": null,
            "right": null
        }
    }
}
the output should be largestValuesInTreeRows(t) = [-1, 7, 1].
##### 나의 풀이 - 큐를 2개를 만들어 사용하였다.
```java
int[] largestValuesInTreeRows(Tree<Integer> t) {
    if(t==null) return new int[]{};
    Queue<Tree> queue1 = new LinkedList<>();
    
    ArrayList<Integer> list = new ArrayList<>();
    queue1.add(t);
    
    while(!queue1.isEmpty()){
        int max = (int) queue1.element().value;
        System.out.println(max+"");
        Queue<Tree> queue2 = new LinkedList<>();
        while(!queue1.isEmpty()){
            Tree<Integer> treeTemp = queue1.poll();
            if(treeTemp.left!=null){
                queue2.add(treeTemp.left);
            }
            if(treeTemp.right!=null){
                queue2.add(treeTemp.right);
            }
            
            if(max<treeTemp.value){
                max = treeTemp.value;
            }            
        }
        list.add(max);
        queue1 = queue2;       
    }
    
    return list.stream().mapToInt(Integer::intValue).toArray();

}
```

##### 전역변수와 재귀함수를 이용한 풀이
```java
List<Integer> r = new ArrayList<>();

List<Integer> largestValuesInTreeRows(Tree<Integer> t) {
    f(0, t);
    return r;
}

void f(int d, Tree<Integer> t) {
    if (t == null) return;
    if (r.size() == d) r.add(-6969);
    if (r.get(d) < t.value) r.set(d, t.value);
    f(d + 1, t.left);
    f(d + 1, t.right);
}
```