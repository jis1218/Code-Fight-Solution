Given a binary tree t and an integer s, determine whether there is a root to leaf path in t such that the sum of vertex values equals s.

```java
boolean hasPathWithGivenSum(Tree<Integer> t, int s) {
    boolean right = false;
    boolean left = false;
    if(t==null){
        if(s==0) return true;
        else return false;
    }
    
    if(t.left!=null)
    left = hasPathWithGivenSum(t.left, s-t.value);
    if(t.right!=null)
    right = hasPathWithGivenSum(t.right, s-t.value);
    if(t.left==null&&t.right==null){
        if(s==t.value) return true;
        else return false;
    }
    
    return left||right;
}
```

##### 다른 풀이
```java
boolean hasPathWithGivenSum(Tree<Integer> root, int s) {
if(root == null && s == 0){
        return true;
    }

    
    if(root == null){
        return false;
    }
    

    
   if(root.value == s && root.left == null && root.right == null)
        return true;
    
    return hasPathWithGivenSum(root.left, s - root.value) || hasPathWithGivenSum(root.right, s - root.value);
}
```