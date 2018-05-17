Note: Your solution should have only one BST traversal and O(1) extra space complexity, since this is what you will be asked to accomplish in an interview.
A tree is considered a binary search tree (BST) if for each of its nodes the following is true:
The left subtree of a node contains only nodes with keys less than the node's key.
The right subtree of a node contains only nodes with keys greater than the node's key.
Both the left and the right subtrees must also be binary search trees.
Given a binary search tree t, find the kth smallest element in it.

clue : 
Try making an in-order traversal of the tree by going down the left branch of the tree first, then counting the current node as visited, then going down the right branch. Keep a count of how many nodes you have seen. Keep in mind that recursion uses stack space. So this will pass the tests, but an iterative solution will be needed to do it in O(1) memory.

Do an iterative in-order traversal (which is hard!) to get the O(1) memory usage. We cannot make paths as visited with an extra field (that would be O(n) memory usage), so you will have to mutate the tree to get under the memory usage limit.

##### 재귀함수를 쓰는 것이 아닌것 같다.

```java
int kthSmallestInBST(Tree<Integer> t, int k) {
    ArrayList<Integer> list = new ArrayList<>();
    find(t, list);
    return list.get(k-1);

}

void find(Tree<Integer> t, ArrayList<Integer> list){
    if(t!=null){
        find(t.left, list);
        list.add(t.value);
        find(t.right, list);
    }
}
```