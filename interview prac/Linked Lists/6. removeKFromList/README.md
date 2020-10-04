Note: Try to solve this task in O(n) time using O(1) additional space, where n is the number of elements in the list, since this is what you'll be asked to do during an interview.
Given a singly linked list of integers l and an integer k, remove all elements from list l that have a value equal to k.
Example
For l = [3, 1, 2, 3, 4, 5] and k = 3, the output should be
removeKFromList(l, k) = [1, 2, 4, 5];
For l = [1, 2, 3, 4, 5, 6, 7] and k = 10, the output should be
removeKFromList(l, k) = [1, 2, 3, 4, 5, 6, 7].
```java
ListNode<Integer> removeKFromList(ListNode<Integer> l, int k) {
    ListNode<Integer> temp;
    while(l!=null && l.value==k){
        if(l.next!=null){
            l = l.next;
        }else{
            l=null;
        }        
    }
    temp = l;
    
    while(temp!=null){
        if(temp.next==null)break;
        if(temp.next.value==k){            
            temp.next = temp.next.next;            
        }else{
           temp = temp.next; 
        }        
    } 
    return l;
}
```

##### 3년만의 다시 풀이
```java
// Singly-linked lists are already defined with this interface:
// class ListNode<T> {
//   ListNode(T x) {
//     value = x;
//   }
//   T value;
//   ListNode<T> next;
// }
//
ListNode<Integer> removeKFromList(ListNode<Integer> l, int k) {
    ListNode<Integer> root = l;
    ListNode<Integer> prev = null;
    while(l!=null){
        if(l.value==k){
            l = l.next;
            if(prev!=null) prev.next = l;
            else root = l;
        }else{
            ListNode<Integer> temp = l;
            l = l.next;
            prev = temp;
        }
    }
    return root;
}
```