
##### 나의 풀이, 전략 - boolean 배열을 만들어 n이 3이라면 (0,1), (0,2), (1,2)의 가능성을 모두 탐색한다. 먼저 0에서 시작할 경우 경유하는 모든 도시를 boolean 배열에 넣어 true로 만들어준다. 그 이후 도착하는 도시가 경유하는 모든 도시를 탐색하여 배열의 값이 true일 경우 2도시는 많게는 1번 경유하여 도착할 수 있다. 만약 그렇지 않을 경우 false를 반환한다.
```java
boolean efficientRoadNetwork(int n, int[][] roads) {
    //boolean 배열을 하나 만든다.
    boolean visited[] = new boolean[n];
    //System.out.println(visited[0]+"");
    
    for(int i=0; i<n-1; i++){
        
        //전부 false로 만들어준다.
        for(int m=0; m<n; m++) visited[m] = false;
        visited[i]=true;
        for(int k=0; k<roads.length; k++){
            if(roads[k][0]==i){
                //System.out.println("i = " + i+", k = " + k+", " + roads[k][1]);
                visited[roads[k][1]]=true;
            }else if(roads[k][1]==i){
                //System.out.println("i = " + i+", k = " + k+", " + roads[k][0]);
                visited[roads[k][0]]=true;
            }
        }
        for(int j=i+1; j<n; j++){
            boolean flag = false;
            for(int q=0; q<roads.length; q++){
                if(roads[q][0]==j){
                    if(visited[roads[q][1]]){
                        //System.out.println("j = " + j+", q = " + q+", " + roads[q][1]);
                        flag = true;
                        break;
                    }
                }else if(roads[q][1]==j){
                    if(visited[roads[q][0]]){
                        //System.out.println("j = " + j+", q = " + q+", " + roads[q][0]);
                        flag = true;
                        break;
                    }
                }
            }    
             if(!flag) return false;
        }
       
    }
    
    return true;

}
```

##### 다른 풀이 - 나와 접근 방법은 비슷
```java
boolean efficientRoadNetwork(int n, int[][] roads) {
    //도시가 1개일 경우 true 리턴
    if (n==1)
        return true;
    
    // 2차원 boolean 배열을 만든다.
    boolean connected[][] = new boolean[n][n];

    // city1과 city2를 지정하여 boolean 배열의 roads값과 그 바꾼 값에 해당 배열값을 true.
    for (int[] road:roads){
        int city1 = road[0];
        int city2 = road[1];
        connected[city1][city2]
            = connected[city2][city1] = true;
    }
    for (int city1 = 0; city1 < n; city1++)
        for (int city2 = 0; city2 < n; city2++){
            if (connected[city1][city2])
                continue;
            boolean found = false;
            for (int t = 0; t < n && !found; t++){
                found |= connected[city1][t] && connected[city2][t];
            }
            if (!found)
                return false;
        }
    return true;
            

}
```