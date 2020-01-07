```java
boolean[][] mergingCities(boolean[][] road) {
    int len = road.length;
    int count = 0;
    int exceptCnt = 0;
    boolean merged[] = new boolean[len];

    for(int i=0; i+1<len; i+=2){
        if(road[i][i+1]){
            merged[i+1] = true;
            exceptCnt++;
            for(int j=0; j<len; j++){
                if(j!=i && j!=i+1){
                    if(road[i+1][j]){
                        road[i][j] = true;
                        road[j][i] = true;                    
                    }
                }
                
            }            
        }       
    }
    
    boolean result[][] = new boolean[len-exceptCnt][len-exceptCnt];
    
    for(int i=0; i<len; i++){
        if(!merged[i]){
            int cnt = 0;
            for(int j=0; j<len; j++){
                if(!merged[j]){
                    result[count][cnt++] = road[i][j];
                } 
            }
            count++;
        }
    }    
    return result;

}
```