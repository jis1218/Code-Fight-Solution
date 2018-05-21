
##### 나의 풀이, sorting이 많이 들어가서 시간이 많이 걸릴 수 밖에 없다. 하지만 배운 점도 있어 만족한다.
##### 1. Arrays의 비교는 Arrays.equals를 이용하자
##### 2. Array를 sorting 할때에는 Collections.sort가 아닌 Arrays.sort를 이용한다.
```java
int[][] roadsBuilding(int cities, int[][] roads) {
    for(int i=0; i<roads.length; i++){
        if(roads[i][0]>roads[i][1]){
            int temp = roads[i][0];
            roads[i][0] = roads[i][1];
            roads[i][1] = temp;
        }
    }
    Arrays.sort(roads, (a,b)->((Comparable)a[1]).compareTo(b[1]));
    Arrays.sort(roads, (a,b)->((Comparable)a[0]).compareTo(b[0]));

    int cnt=0;
    ArrayList<int[]> list = new ArrayList<>();
    int i=0;
    int j=i+1;
    
    while(i<cities-1){
        if(Arrays.equals(new int[]{i, j}, roads[cnt])){
            cnt = Math.min(cnt+1, roads.length-1);
            j++;
            if(j==cities){
                i++;
                j = i+1;
            }
        }else{
            list.add(new int[]{i, j});
            j++;
            if(j==cities){
                i++;
                j = i+1;
            }
        }
    }
    
    return list.toArray(new int[0][]);

}
```
##### boolean을 이용한 좋은 풀이이다.
```java
int[][] roadsBuilding(int cities, int[][] roads) {
    
    int count = (cities * (cities - 1)) / 2;
    
    boolean[][] matrix = new boolean[cities][cities];
    for (int[] road : roads) {
        matrix[road[0]][road[1]] = true;
        matrix[road[1]][road[0]] = true;
        count--;
    }           
               
    int[][] result = new int[count][2];
    int index = 0;
        
    for (int i = 0; i < cities; i++) {
        for (int j = i + 1; j < cities; j++) {
            if (!matrix[i][j]) {
                result[index][0] = i;
                result[index][1] = j;
                index++;
            }
        }
    }
    
    return result;
}
```