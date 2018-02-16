Given a singly linked list of integers, determine whether or not it's a palindrome.
Example
For l = [0, 1, 0], the output should be
isListPalindrome(l) = true;
For l = [1, 2, 2, 3], the output should be
isListPalindrome(l) = false.

##### 나의 풀이

```java
boolean isListPalindrome(ListNode<Integer> l) {
    
    ListNode prev;
    int size = 0;
    ArrayList<Integer> list = new ArrayList<>();
    
    while(l!=null){     
        list.add(l.value);
        l = l.next;
    }
    
    for(int i =0; i<=list.size()-i-1; i++){
        //System.out.println(list.get(i) + ", " + (list.get(list.size()-i-1)) );
        if((double)list.get(i)!=(double)list.get(list.size()-i-1)) return false;        
    }
    
    return true;
}
```

##### 다른 사람의 풀이(ArrayList나 아래에서 얘기하는 internal function 등을 쓰지 않았다. slow와 fast 개념을 도입함)
```
/* Basic idea: 
 * - Find the center point of the node list, using double steps (fast var) and 
 *   reverse the first half of the list.
 * - Walk on the second half and walk back in the first to the first difference.
 * - Return false if found diff, or true if all items are equal.
 */
function isListPalindrome(list) {
    var slow = null,
        fast = list,
        temp;
    // Find center point and reverse the first half of the list
    while (fast && fast.next) {
        fast = fast.next.next;
        temp = list.next;
        list.next = slow;
        slow = list;
        list = temp;
    }
    // If fast not null, list length is odd, ignore the center value
    if (fast) {
        list = list.next;
    }
    // Find the first difference
    while (list) {
        if (slow.value != list.value) return false;
        slow = slow.next;
        list = list.next;
    }
    // Return true, if no diff
    return true;
}

/* Using recursion O(n) solution and 2 extra variables and lot of stack. */
function isListPalindrome2(l) {
    var r = l,
        ret,
        f = v => 
            r ? (r = r.next, ret = !r || f(r.value) && l.value == v, l = l.next, ret)
              : 1;
    return !r || f(r.value);
}

/* The shortest solution. But using internal functions and lot of memory: */
function isListPalindrome3(l) {
    l = JSON.stringify(l).slice(1,-1).split`,`;
    return l + "" == l.reverse();
}
```

```java
boolean isListPalindrome(ListNode<Integer> l) {
    // 1. Move
    ListNode slow = l, fast = l; 
    while(fast != null && fast.next != null){
        slow = slow.next; 
        fast = fast.next.next; 
    }
    
    // linked list has odd length
    if(fast!=null){
        slow = slow.next; 
    }

    // 2. Reverse second half of linked list and move slow pointer to the 2nd head
    slow = reverse(slow); 
    fast = l; 
    // 3. Compare
    while(slow!=null){
 
        if(!fast.value.equals(slow.value)){
            System.out.println(slow.value);
            System.out.println(fast.value); 
            return false; 
        }
        fast = fast.next; 
        slow = slow.next; 
    }
    return true; 
}

public ListNode reverse(ListNode<Integer> head){
    ListNode prev = null; 
    while(head!=null){
        ListNode next = head.next; 
        head.next = prev; 
        prev = head; 
        head = next; 
    }
    return prev; 
}
```