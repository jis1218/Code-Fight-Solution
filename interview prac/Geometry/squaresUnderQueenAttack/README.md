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