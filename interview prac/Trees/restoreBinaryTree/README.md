Note: Your solution should have O(inorder.length) time complexity, since this is what you will be asked to accomplish in an interview.
Let's define inorder and preorder traversals of a binary tree as follows:
Inorder traversal first visits the left subtree, then the root, then its right subtree;
Preorder traversal first visits the root, then its left subtree, then its right subtree.
For example, if tree looks like this:
    1
   / \
  2   3
 /   / \
4   5   6
then the traversals will be as follows:
Inorder traversal: [4, 2, 1, 5, 3, 6]
Preorder traversal: [1, 2, 4, 3, 5, 6]
Given the inorder and preorder traversals of a binary tree t, but not t itself, restore t and return it.

##### 핵심은 Array를 나눠 recursive하게 진행하는 것이다.
```java
Tree<Integer> restoreBinaryTree(int[] inorder, int[] preorder) {
    System.out.println(inorder.length + ", " + preorder.length);
    if(preorder.length==0) return null;
    Tree<Integer> root = new Tree(preorder[0]);
    int inorderIndex = 0;
    for(int i=0; i<inorder.length; i++){
        if(inorder[i]==preorder[0]) inorderIndex = i;
    }
    
    int[] leftInorder = Arrays.copyOfRange(inorder, 0, inorderIndex);
    int[] rightInorder = Arrays.copyOfRange(inorder, inorderIndex+1, inorder.length);
    int[] leftPreorder = Arrays.copyOfRange(preorder, 1, 1+inorderIndex);
    int[] rightPreorder = Arrays.copyOfRange(preorder, 1+inorderIndex, preorder.length);
    
    root.left = restoreBinaryTree(leftInorder, leftPreorder);
    root.right = restoreBinaryTree(rightInorder, rightPreorder);
    
    return root;    
    
}
```

##### 첫번째 풀이
```java
Tree<Integer> restoreBinaryTree(int[] inorder, int[] preorder) {
    list = new ArrayList<>();
    for(int i=0; i<preorder.length; i++){
        list.add(preorder[i]);
    }
    return makeTree(inorder, 0, inorder.length-1);
    
}

ArrayList<Integer> list;

Tree<Integer> makeTree(int[] inorder, int start, int end){
    if(list.size()==0) return null;
    Tree<Integer> tree = new Tree(list.get(0));
    if(start>end) return null;
    int inorderIndex = 0;
    for(int i=start; i<=end; i++){
        if(list.get(0)==inorder[i]){
            inorderIndex = i;
        }
    }
    list.remove(0);
    tree.left = makeTree(inorder, start, inorderIndex-1);    
    tree.right = makeTree(inorder, inorderIndex+1, end);

    return tree; 
    
}
```