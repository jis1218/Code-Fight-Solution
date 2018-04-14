##### 시간초과 때문에 애를 많이 먹은 문제
```java
    static int[] climbingLeaderboard(int[] scores, int[] alice) {
        /*
         * Write your code here.
         */
        int result[] = new int[alice.length];
        int index = 0;
        int overlapp = 0;
        //int rank = 1;
        for(int i=alice.length-1; i>=0; i--){
            for(int j=index; j<scores.length; j++){
                if(j!=0 && (scores[j-1]==scores[j])){
                    overlapp++;
                }
                if(scores[j]<=alice[i]){
                    index = j;
                    break;                   
                }else if(j==scores.length-1){
                    index = j+1;
                }
            }
            result[i]=index+1-overlapp;
        }        
        return result;  

    }
```

##### 그 전 풀이는 이랬다.
```java
    static int[] climbingLeaderboard(int[] scores, int[] alice) {
        /*
         * Write your code here.
         */
        int result[] = new int[alice.length];
        int index = 0;
        int overlapp = 0;
        int rank = 1;
        for(int i=alice.length-1; i>=0; i--){
            for(int j=index; j<scores.length; j++){
                if(j!=0 && (scores[j-1]==scores[j])){
                    overlapp++;
                }
                if(scores[j]<=alice[i]){
                    index = j;
                    break;                   
                }else{
                    rank++;
                }
            }
            result[i]=rank-overlapp;
        }        
        return result;   
    }
```

##### 결국 변수와 그것을 더해주는 연산이 있으므로 해서 시간이 더 걸린다.