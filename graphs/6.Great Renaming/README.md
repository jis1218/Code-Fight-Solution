Once upon a time, in a kingdom far, far away, there lived a king Byteasar VI. As any king with such a magnificent name, he was destined to leave a trace in history. Unfortunately imagination wasn't one of king Byteasar's strong suits, so the reform he came up with was quite simple: the king ordered to rename all the cities. He didn't want to come up with new names (as a king, he'd have to remember them all!), so he ordered the cities to swap their names in such manner that the ith city would have the name of the city number (i + 1)th. The last city in the Byteasar's kingdom would, naturally, get the name of the very first city.
The cartographers were not happy with this reform, since they had to redraw all the maps of the kingdom. Before the reform, information about all the roads between the cities were stored in the roadRegister. Prior to drawing maps, they had to start with updating the register. Your task is to find out what the updated register looked like.
Example
For
roadRegister = [[false, true,  true,  false],
                [true,  false, true,  false],
                [true,  true,  false, true ],
                [false, false, true,  false]]
the output should be
greatRenaming(roadRegister) = [[false, false, false, true ],
                               [false, false, true,  true ],
                               [false, true,  false, true ],
                               [true,  true,  true,  false]]

##### in-place로 풀었다.
```java
boolean[][] greatRenaming(boolean[][] roadRegister) {
    int n = roadRegister.length;
    for(int i=0; i<roadRegister.length; i++){
        boolean temp = roadRegister[i][n-1];
        for(int j=n-1; j>=1; j--){            
            roadRegister[i][j] = roadRegister[i][j-1];            
        }
        roadRegister[i][0] = temp;
    }

    for(int i=0; i<roadRegister.length; i++){
        boolean temp = roadRegister[n-1][i];
        for(int j=n-1; j>=1; j--){            
            roadRegister[j][i] = roadRegister[j-1][i];            
        }
        roadRegister[0][i] = temp;
    }
    
    return roadRegister;

}
```

##### 다른 풀이, 메모리를 조금 사용하였따.
```java
boolean[][] greatRenaming(boolean[][] roadRegister) {
    int n = roadRegister.length;
    if(n == 1) return roadRegister;
    boolean[][] renamed = new boolean[n][n];
    for(int i = 0; i < n; i++) {
        for(int j = 0; j < n; j++) {
            renamed[(i+1)%n][(j+1)%n] = roadRegister[i][j];
        }
    }
    return renamed;
}
```