You are given the root of a binary search tree (BST), where the values of exactly two nodes of the tree were swapped by mistake. Recover the tree without changing its structure.

##### 가장 많이 추천 받은 풀이와 거의 비슷한 걸 보니 잘 푼듯 한데 space complexity가 O(1)이 아닌듯??

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public void recoverTree(TreeNode root) {
        helper(root);     
        int temp = prev.val;
        prev.val = max.val;
        max.val = temp;
    }
    
    private TreeNode prev = null;
    private TreeNode max = null;
    
    private void helper(TreeNode node) {
        if(node==null) return;        
        helper(node.left);
        if(prev == null || (prev.val < node.val && max == null)) {
            prev = node;
        }else if(prev.val > node.val) {
            max = node;
        }
        
        helper(node.right);
    }
}
```