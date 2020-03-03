Note: Write a solution with O(operations.length) complexity, since this is what you would be asked to do during a real interview.

Implement a modified stack that, in addition to using push and pop operations, allows you to find the current minimum element in the stack by using a min operation.

Example

For operations = ["push 10", "min", "push 5", "min", "push 8", "min", "pop", "min", "pop", "min"], the output should be
minimumOnStack(operations) = [10, 5, 5, 5, 10].
##### Stack과 Heap을 이용하여 문제를 풀었다.
```java
int[] minimumOnStack(String[] o) {
    Queue<Integer> q = new PriorityQueue(3);
    List<Integer> l = new ArrayList<>();
    Stack<Integer> st = new Stack<>();
    for(String s : o){
        String t = s.substring(0,2);
        int i=0;
        if(t.equals("pu")){
            i = Integer.valueOf(s.split(" ")[1]);
            st.push(i);
            q.add(i);
        }else if(t.equals("mi")){
            l.add(q.peek());
        }else{
            i = st.pop();
            q.remove(i);
        }
    }
    return l.stream().mapToInt(i->i).toArray();
}
```