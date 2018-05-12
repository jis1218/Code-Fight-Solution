Note: Your solution should have O(n) time complexity, where n is the number of element in l, and O(1) additional space complexity, since this is what you would be asked to accomplish in an interview.
Given a linked list l, reverse its nodes k at a time and return the modified list. k is a positive integer that is less than or equal to the length of l. If the number of nodes in the linked list is not a multiple of k, then the nodes that are left out at the end should remain as-is.
You may not alter the values in the nodes - only the nodes themselves can be changed.
Example
For l = [1, 2, 3, 4, 5] and k = 2, the output should be
reverseNodesInKGroups(l, k) = [2, 1, 4, 3, 5];
For l = [1, 2, 3, 4, 5] and k = 1, the output should be
reverseNodesInKGroups(l, k) = [1, 2, 3, 4, 5];
For l = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11] and k = 3, the output should be
reverseNodesInKGroups(l, k) = [3, 2, 1, 6, 5, 4, 9, 8, 7, 10, 11].

##### 정말 오래 걸린 문제... 하지만 해냈고 다른 풀이보다 깔끔하게 푼 것 같아 기분이 좋다.

```java
ListNode<Integer> reverseNodesInKGroups(ListNode<Integer> l, int k) {
   
    ListNode<Integer> prev = null;
    ListNode<Integer> temp = null;
    ListNode<Integer> veryEnd = null;
    ListNode<Integer> confirm = null;
    
    confirm = l;
    veryEnd = l;
    
    //만약 k에 못미칠 경우 그대로 l을 반환해 준다.
    for(int i=0; i<k; i++){
        if(confirm==null) return l;
        confirm = confirm.next;        
    } 
    
    //LinkedList 거꾸로 해주는 코드
    for(int i=0; i<k && l!=null; i++){
        temp = l.next;
        l.next = prev;
        prev = l;
        l = temp;        
    }
    //veryEnd는 끝으로 가는 맨 처음 노드를 항상 가리키므로
    veryEnd.next = reverseNodesInKGroups(l, k);
    
    return prev; 
}
```