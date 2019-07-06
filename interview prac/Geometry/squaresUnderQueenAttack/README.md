```java

boolean[] squaresUnderQueenAttack(int n, int[][] queens, int[][] queries) {
    
    boolean[][] boards = new boolean[n][n];
    boolean result[] = new boolean[queries.length];
    
    for(int i=0; i<queens.length; i++){
        int first=queens[i][0];
        int second=queens[i][1];
        //first line
        int temp1=0;
        int temp2=0;
        int temp3=0;
        int temp4=0;
        if(first>=second){
            temp3=first-second;
            temp4=0;
        }else{
            temp3=0;
            temp4=second-first;
        }

        while(temp1<n||temp2<n){
            if(temp1<n){
                boards[first][temp1]=true;
                temp1++;
            }
            if(temp2<n){
                boards[temp2][second]=true;
                temp2++;
            } 
            if(temp3+temp1<n && temp4+temp2<n){
                boards[temp3+temp1][temp4+temp2]=true;
            }
        }
        temp1=0;
        temp2=0;
        boolean flag1=true;
        boolean flag2=true;
        while(flag1||flag2){
            if(first+temp1<n && second-temp2>=0){
                boards[first+temp1][second-temp2]=true;
            }else flag1=false;
            if(first-temp1>=0 && second+temp2<n){
                boards[first-temp1][second+temp2]=true;
            }else flag2=false;
            temp1++;
            temp2++;
        }
    }
    for(int i=0; i<queries.length; i++){
        result[i] = boards[queries[i][0]][queries[i][1]];
    }
    return result;

}

```

##### 좀 개선된 풀이 - 하지만 여전히 실패...
```java

boolean[] squaresUnderQueenAttack(int n, int[][] queens, int[][] queries) {    
    
    HashSet<String> map = new HashSet<>();
    boolean result[] = new boolean[queries.length];
    
    for(int i=0; i<queens.length; i++){
        int first=queens[i][0];
        int second=queens[i][1];

        int temp1=0;

        while(temp1<n){
            map.add((first + ", " + temp1));
            map.add((temp1 + ", " + second));
             
            if(first-second+temp1>=0 && first-second+temp1<n && temp1<n){
                map.add((first-second+temp1 + ", " + temp1));
            }
            if(first+second-temp1>=0 && first+second-temp1<n){
                map.add((first+second-temp1 + ", " + temp1));
            }            
            temp1++;
        }        
    }
    for(int i=0; i<queries.length; i++){
        result[i] = map.contains((queries[i][0] + ", " + queries[i][1]));
    }
    return result;

}
```

##### 이방법이 위에 방법보다 빠르긴 했다
```java
boolean[] squaresUnderQueenAttack(int n, int[][] queens, int[][] queries) { 
    boolean result[] = new boolean[queries.length];    
    for(int i=0; i<queries.length; i++){
        int c = queries[i][0];
        int d = queries[i][1];
        for(int j=0; j<queens.length; j++){
            int a = queens[j][0];
            int b = queens[j][1];   
            if(a-c==0 || b-d==0 || Math.abs(a-c)==Math.abs(b-d)){
                result[i]=true;
                break;
            }
        }
    }
    return result;
}
```

##### HashSet을 이용해 조금이라도 연산시간을 줄여준다.
```java
boolean[] squaresUnderQueenAttack(int n, int[][] queens, int[][] queries) { 
    boolean result[] = new boolean[queries.length];  
    HashSet<Integer> set1 = new HashSet<>();
    HashSet<Integer> set2 = new HashSet<>();
    for(int i=0; i<queens.length; i++){
        set1.add(queens[i][0]);
        set2.add(queens[i][1]);
    }
    
    for(int i=0; i<queries.length; i++){
        int c = queries[i][0];
        int d = queries[i][1];
        if(set1.contains(c) || set2.contains(d)){
            result[i]=true;
            continue;
        }
        for(int j=0; j<queens.length; j++){
            int a = queens[j][0];
            int b = queens[j][1];
            
            if(Math.abs(a-c)==Math.abs(b-d)){
                result[i]=true;
                break;
            }
        }
    }
    return result;
}
```

##### 좋은 풀이 - 대각선의 합이 항상 같음을 이용한다...
```java
boolean[] squaresUnderQueenAttack(int n, int[][] queens, int[][] queries) {
    boolean[] rows = new boolean[n];
    boolean[] columns = new boolean[n];
    boolean[] diag = new boolean[n*2];
    boolean[] diag2 = new boolean[n*2];
    
    for (int[] q : queens) {
        int c = q[0];
        int r = q[1];
        rows[r] = true;
        columns[c] = true;
        diag[n+c-r-1] = true;
        diag2[c+r] = true;
    }
    
    boolean[] result = new boolean[queries.length];
    int i = 0;
    for (int[] q : queries) {
        int c = q[0];
        int r = q[1];
        result[i++] = rows[r] || columns[c] || diag[n+c-r-1] || diag2[c+r];
    }
    return result;
}
```
