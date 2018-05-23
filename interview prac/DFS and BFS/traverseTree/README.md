Note: Try to solve this task without using recursion, since this is what you'll be asked to do during an interview.
Given a binary tree of integers t, return its node values in the following format:
The first element should be the value of the tree root;
The next elements should be the values of the nodes at height 1 (i.e. the root children), ordered from the leftmost to the rightmost one;
The elements after that should be the values of the nodes at height 2 (i.e. the children of the nodes at height 1) ordered in the same way;
Etc.


##### 어려운 문제는 아니었음
```java
int[] traverseTree(Tree<Integer> t) {
    if(t==null) return new int[]{};
    Queue<Tree> queue = new LinkedList<>();
    ArrayList<Integer> list = new ArrayList<>();
    
    queue.add(t);
    
    while(!queue.isEmpty()){
        Tree<Integer> temp = queue.remove();
        list.add(temp.value);
        if(temp.left!=null){
            queue.add(temp.left);
        }
        if(temp.right!=null){
            queue.add(temp.right);
        }
    }
    System.out.print(list.size());
    int result[] = new int[list.size()];
    for(int i=0; i<list.size(); i++) result[i] = list.get(i);
    return result;

}
```

###### Integer list를 int array로 바꿔주는 방법
```java
result.stream().mapToInt(Integer::intValue).toArray();
```