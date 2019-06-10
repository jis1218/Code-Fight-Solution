```java
int[] nextLarger(int[] a) {
    Stack<Integer> stack = new Stack<>();
    int[] result = new int[a.length];
    
    for(int i = a.length-1; i>=0; i--){
        if(stack.empty()){
            result[i] = -1;
            stack.push(a[i]);
        }else{
            boolean flag = true;
          while(a[i]>stack.peek()){
            stack.pop();
              if(stack.empty()){
                  result[i] = -1;
                  stack.push(a[i]);
                  flag = false;
                  break;
              }
            }
            if(flag){
               result[i] = stack.peek();
                stack.push(a[i]); 
            }
            
        }
    }
    return result;

}
```