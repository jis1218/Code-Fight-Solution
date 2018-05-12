Note: Try to solve this task in O(list size) time using O(1) additional space, since this is what you'll be asked during an interview.
Given a singly linked list of integers l and a non-negative integer n, move the last n list nodes to the beginning of the linked list.
Example
For l = [1, 2, 3, 4, 5] and n = 3, the output should be
rearrangeLastN(l, n) = [3, 4, 5, 1, 2];
For l = [1, 2, 3, 4, 5, 6, 7] and n = 1, the output should be
rearrangeLastN(l, n) = [7, 1, 2, 3, 4, 5, 6].

```java
ListNode<Integer> rearrangeLastN(ListNode<Integer> l, int n) {
    ListNode<Integer> last = l, prev = l, temp = null;
    
    if(n==0) return l;
    
    for(int i=0; i<n; i++) last = last.next;
    
    if(last==null) return l;
    
    while(last.next!=null){
        prev = prev.next;
        last = last.next;
    }    
    
    temp = prev.next;
    prev.next = null;
    last.next = l;
    
    return temp;  
}
```