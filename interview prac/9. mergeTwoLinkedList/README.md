Given two singly linked lists sorted in non-decreasing order, your task is to merge them. In other words, return a singly linked list, also sorted in non-decreasing order, that contains the elements from both original lists.
Example
For l1 = [1, 2, 3] and l2 = [4, 5, 6], the output should be
mergeTwoLinkedLists(l1, l2) = [1, 2, 3, 4, 5, 6];
For l1 = [1, 1, 2, 4] and l2 = [0, 3, 5], the output should be
mergeTwoLinkedLists(l1, l2) = [0, 1, 1, 2, 3, 4, 5].
##### 나의 풀이 - null체크를 따로 해줘야 해서 코드가 길어짐, 중복되는 코드를 한번에 합칠 수 없을까?
```java
ListNode<Integer> mergeTwoLinkedLists(ListNode<Integer> l1, ListNode<Integer> l2) {
    ListNode<Integer> node = new ListNode(0); //새로운 ListNode를 하나 만들어줌
    ListNode<Integer> result = node; //result라는 List에 node를 넣어줌
    
    while(l1!=null || l2!=null){
        
        // 어느 한쪽이 null일 때 실행되는 함수
        if(l1==null){
            node.next = new ListNode(l2.value);
            l2 = l2.next;
            node = node.next;
            continue;
        }else if(l2==null){
            node.next = new ListNode(l1.value);
            l1 = l1.next;
            node = node.next; 
            continue;
        }

        // l1과 l1중 큰 수를 node에 넣어준다.
        if(l1.value<=l2.value){
            node.next = new ListNode(l1.value);
            l1 = l1.next;
            node = node.next;            
        }else if(l1.value>=l2.value){
            node.next = new ListNode(l2.value);
            l2 = l2.next;
            node = node.next;
        }   
    }    
    return result.next;
}
```
##### 다른 사람의 풀이 - 재귀함수를 이용해 간단하게 표현했다.
```java
ListNode<Integer> mergeTwoLinkedLists(ListNode<Integer> l1, ListNode<Integer> l2) {
    if(l1==null) return l2;
    if(l2==null) return l1;
    if(l1.value<l2.value) {
        l1.next = mergeTwoLinkedLists(l1.next,l2);
        return l1;
    }
    
    else {
        l2.next = mergeTwoLinkedLists(l1,l2.next);
        return l2;
    }
}
```