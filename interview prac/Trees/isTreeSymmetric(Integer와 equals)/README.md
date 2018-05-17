Given a binary tree t, determine whether it is symmetric around its center, i.e. each side mirrors the other.

##### 핵심은 노드와 노드를 바꿔치기 하는 것, 그리고 Integer 객체는 비교할 때 ==이 아닌 equals를 사용해야 한다는 것이다.

```java
boolean isTreeSymmetric(Tree<Integer> t) {
    if(t==null) return true;
    if(t.left==null && t.right==null) return true;
    if(t.left==null || t.right==null) return false;
    else if(!t.left.value.equals(t.right.value)) return false;
    
    Tree<Integer> temp = t.left.right;
    t.left.right = t.right.right;
    t.right.right = temp;

    return isTreeSymmetric(t.left)&&isTreeSymmetric(t.right);    
}
```

##### 다른 사람의 풀이 - 나처럼 바꾸지 않고 메서드를 하나 더 만들어서 사용하였다.
```java
boolean isTreeSymmetric(Tree<Integer> t) {
    if (t == null) {
        return true;
    }
    return helper(t.left, t.right);
}
boolean helper(Tree<Integer> left, Tree<Integer> right) {
    //base case
    if (left == null && right == null) {
        return true;
    }
    if (left == null || right == null) {
        return false;
    }
    // ask a boolean from left, a boolean from right and return result upwards
    return (left.value.equals(right.value)) && helper(left.left, right.right) && helper(left.right, right.left);
}
```
```java
boolean isTreeSymmetric(Tree<Integer> t) {
    if (t == null) return true;
    return compare(t.left, t.right);
}

boolean compare(Tree<Integer> left, Tree<Integer> right) {
    if (left == null && right == null) return true;
    if (left == null || right == null) return false;
    if (!left.value.equals(right.value)) return false;
    return compare(left.left, right.right) && compare(left.right, right.left);
}
```
