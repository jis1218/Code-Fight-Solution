ListNode를 거꾸로 만들어주는 재귀함수
```java
ListNode<Integer> addTwoHugeNumbers(ListNode<Integer> a, ListNode<Integer> b) {
    ListNode<Integer> first = new ListNode(0);
    
    test(a, first);   
    
    return first;
}

ListNode<Integer> test(ListNode<Integer> a, ListNode<Integer> first){
    ListNode newNode = null;
    if(a!=null){
        newNode = new ListNode(a.value);
        test(a.next, first).next = newNode;        
        System.out.println(a.value);  
        
        return newNode;
    }    
    return first;
}
```

##### 이것이 답이 나온 최종 풀이이긴 하나 마음에 들지는 않는다. 다른 풀이를 보니 보통 reverse 하였는데 reverse 하는 방법이 나랑 다르다. 그래서 reverse 하는 다른 방법을 더 공부해야 한다.

```java
ListNode<Integer> addTwoHugeNumbers(ListNode<Integer> a, ListNode<Integer> b) {
    ListNode<Integer> first  = new ListNode(0);
    ListNode<Integer> second = new ListNode(0);
    ListNode<Integer> result = new ListNode(0);
    ListNode<Integer> target = result;
    

    reverse(a, first);
    reverse(b, second);
    int add = 0;
    
    while(true){
        int sum1 = 0;
        int sum2 = 0;
        if(first!=null){
            sum1 = first.value;
        }
        if(second!=null){
            sum2 = second.value;
        }
        
        int sum = sum1 + sum2 + add;
        if(sum>9999){
            sum = sum - 10000;
            add = 1;
        }else{
            if(first==null && second == null && sum==0) break;
            add = 0;
        }
        ListNode<Integer> temp = new ListNode(sum);
        result.next = temp;
        result = result.next;

        if(first!=null) first = first.next;
        if(second!=null) second = second.next;
        
    }
    ListNode<Integer> realResult = new ListNode(0);
    reverse(target.next.next, realResult);
    
    return realResult.next; 
}

ListNode<Integer> reverse(ListNode<Integer> a, ListNode<Integer> k){
    if(a!=null){   
        ListNode<Integer> newNode = new ListNode(a.value);
        reverse(a.next, k).next = newNode;
        
        return newNode;
    }       
    return k;    
}
```

##### 다른 풀이
```java
ListNode<Integer> addTwoHugeNumbers(ListNode<Integer> a, ListNode<Integer> b) {
   ListNode<Integer> result = new ListNode<Integer>(0);
	    ListNode<Integer> head = result;
	    int carry=0;
	    a= reverse(a);
	    b= reverse(b); 
	    while(a!=null || b!=null){
	        if(a!=null){
	            carry+= a.value;
	            a=a.next;
	        }
	        if(b!=null){
	            carry+=b.value;
	            b= b.next;
	        }
	        head.next = new ListNode<Integer>(carry%10000);
	        head = head.next;
	        carry = carry/10000;
	    }
	    if(carry>=1)
	        head.next= new ListNode<Integer>(carry);
	    
	    return reverse(result.next);
	    
	}

	ListNode<Integer> reverse(ListNode<Integer> head){
	    ListNode<Integer> prev =null;
	    while(head!=null){
	        ListNode<Integer> temp = head.next;
	        head.next= prev;
	        prev= head;
	        head= temp;
	    }
	    return prev;
	}
```