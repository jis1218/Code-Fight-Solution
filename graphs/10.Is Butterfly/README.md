```java
boolean isButterfly(boolean[][] adj) {
    int garo[] = new int[5];
    int sero[] = new int[5];
    int center = -1;
    for(int i=0; i<5; i++){
        for(int j=0; j<5; j++){
            if(adj[i][j]){
                garo[i]++;
                sero[j]++;
            }
        }
        if(garo[i]==4) center = i;
    }
    if(center==-1) return false;
    int a = 0;
    int b = 0;



    for(int i=0; i<5; i++){
        if(adj[i][i]) return false;
        if(garo[i]==4){
            if(sero[i]!=4 || adj[i][i]) return false;
            a++;
        }
        if(garo[i]==2){
            if(!adj[i][center]) return false;
            if(sero[i]!=2) return false;
            b++;
        }
    }
    
    return a==1 && b==4;


}
```
##### 너무 어렵게 푼 느낌