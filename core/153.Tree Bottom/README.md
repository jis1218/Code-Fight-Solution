You are given a recursive notation of a binary tree: each node of a tree is represented as a set of three elements:

value of the node;
left subtree;
right subtree.
So, a tree can be written as (value left_subtree right_subtree). It is guaranteed that 1 ≤ value ≤ 109. If a node doesn't exist then it is represented as an empty set: (). For example, here is a representation of a tree in the given picture:

```java
int[] treeBottom(String tree) {
    int depth = 0;    
    String num = "";
    ArrayList<Node> list = new ArrayList<>();
    for(int i=0; i<tree.length(); i++){
        char temp = tree.charAt(i);
        if(temp=='('){
            num = "";
            depth++;
        }else if(temp>='0' && temp<='9'){
            num += temp;
        }else if(temp==' ' && !num.equals("")){
            list.add(new Node(Integer.valueOf(num), depth));
        }else if(temp==')'){
            depth--;
        }
    }
    int max = 0;
    ArrayList<Integer> result = new ArrayList<>();
    for(int i=0; i<list.size(); i++){
        if(list.get(i).depth==max){
            result.add(list.get(i).value);
        }else if(list.get(i).depth>max){
            result.clear();
            result.add(list.get(i).value);
            max = list.get(i).depth;
        }
    }

    return result.stream().mapToInt(i -> i).toArray();
}

class Node{
    int value;
    int depth;
    Node(int value, int depth){
        this.value = value;
        this.depth = depth;
    }
}
```

##### 위의 풀이를 더 줄여봄
```java
int[] treeBottom(String tree) {
    int depth = 0;    
    String num = "";
    int max=0;
    ArrayList<Integer> result = new ArrayList<>();
    for(int i=0; i<tree.length(); i++){
        char temp = tree.charAt(i);
        if(temp=='('){
            num = "";
            depth++;
        }else if(temp>='0' && temp<='9'){
            num += temp;
        }else if(temp==' ' && !num.equals("")){
            if(max==depth){
                result.add(Integer.valueOf(num));
            }else if(max<depth){
                max = depth;
                result.clear();
                result.add(Integer.valueOf(num));
            }
            
        }else if(temp==')'){
            depth--;
        }
    }    

    return result.stream().mapToInt(i -> i).toArray();
}
```