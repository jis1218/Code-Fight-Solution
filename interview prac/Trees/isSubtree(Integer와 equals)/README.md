Given two binary trees t1 and t2, determine whether the second tree is a subtree of the first tree. A subtree for vertex v in a binary tree t is a tree consisting of v and all its descendants in t. Determine whether or not there is a vertex v (possibly none) in tree t1 such that a subtree for vertex v (possibly empty) in t1 equals t2.
Example
This is what these trees look like:
      t1:             t2:
       5              10
      / \            /  \
    10   7          4    6
   /  \            / \    \
  4    6          1   2   -1
 / \    \
1   2   -1
the output should be isSubtree(t1, t2) = true.
As you can see, t2 is a subtree of t1 (the vertex in t1 with value 10).

This is what these trees look like:
        t1:            t2:
         5             10
       /   \          /  \
     10     7        4    6
   /    \           / \    \
  4     6          1   2   -1
 / \   / 
1   2 -1
As you can see, there is no vertex v such that the subtree of t1 for vertex v equals t2.
the output should be isSubtree(t1, t2) = false.

```java
boolean isSubtree(Tree<Integer> t1, Tree<Integer> t2) {
    if(t1==null && t2==null) return true;
    if(t1==null) return false;
    if(t2==null) return true;
    System.out.println(t1.value+"");
    if(t1.value.equals(t2.value)){
        if(check(t1, t2)){
            return true;
        }
    }
    
    return isSubtree(t1.left, t2) || isSubtree(t1.right, t2) ;
}

boolean check(Tree<Integer> t1, Tree<Integer> t2){
    if(t1==null && t2==null) return true;
    if((t1==null && t2!=null) || (t2==null && t1!=null)) return false;
    if(t1.value.equals(t2.value)){
        return check(t1.left, t2.left) && check(t1.right, t2.right);
    }else{
        return false;
    }
}