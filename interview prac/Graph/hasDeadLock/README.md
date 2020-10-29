```java
boolean hasDeadlock(int[][] connections) {
    boolean[] isVisit = new boolean[connections.length];
    for(int i=0; i<connections.length; i++){
        if(!isVisit[i]){
            helper(connections, isVisit, new HashSet<Integer>(), i);
            System.out.println("=======");            
        }
        if(flag) return true;
    }
    return flag;
}
boolean flag = false;
void helper(int[][] connections, boolean[] isVisit, HashSet<Integer> set, int num){
    if(flag) return;
    if(set.contains(num)){
        //System.out.println("contain = " + num);
        flag = true;
        return;
    }
    set.add(num);
    System.out.print(num + ", ");
    for(int i=0; i<connections[num].length; i++){
        if(!isVisit[connections[num][i]]){
            isVisit[connections[num][i]] = true;
            helper(connections, isVisit, set, connections[num][i]);
            isVisit[connections[num][i]] = false;
            //System.out.print(" ****** ");
            if(flag) return;
        }
    }
    set.remove(num);    
}
```
