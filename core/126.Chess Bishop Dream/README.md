In ChessLand there is a small but proud chess bishop with a recurring dream. In the dream the bishop finds itself on an n × m chessboard with mirrors along each edge, and it is not a bishop but a ray of light. This ray of light moves only along diagonals (the bishop can't imagine any other types of moves even in its dreams), it never stops, and once it reaches an edge or a corner of the chessboard it reflects from it and moves on.
Given the initial position and the direction of the ray, find its position after k steps where a step means either moving from one cell to the neighboring one or reflecting from a corner of the board.
Example
For boardSize = [3, 7], initPosition = [1, 2],
initDirection = [-1, 1] and k = 13, the output should be
chessBishopDream(boardSize, initPosition, initDirection, k) = [0, 1].
Here is the bishop's path:
[1, 2] -> [0, 3] -(reflection from the top edge)-> [0, 4] -> 
[1, 5] -> [2, 6] -(reflection from the bottom right corner)-> [2, 6] ->
[1, 5] -> [0, 4] -(reflection from the top edge)-> [0, 3] ->
[1, 2] -> [2, 1] -(reflection from the bottom edge)-> [2, 0] -(reflection from the left edge)->
[1, 0] -> [0, 1]

##### 최종 답 - 함수로 간추릴 수도 있을 듯, for문을 안썼기 때문에 O(1) 시간이 걸릴 것 같다.
```java
int[] chessBishopDream(int[] boardSize, int[] initPosition, int[] initDirection, int k) {
    int net = k%(boardSize[1]*2);
    if(initDirection[1]==1){
        if(net<boardSize[1]-initPosition[1]){
            initPosition[1] += net;
        }else if(net<boardSize[1]*2-initPosition[1]){
            initPosition[1] = 2*boardSize[1]-net-initPosition[1]-1;
        }else{
            initPosition[1] = initPosition[1]-(2*boardSize[1]-net);
        }
    }else{
        if(net<initPosition[1]+1){
            initPosition[1] -= net;
        }else if(net<boardSize[1]+initPosition[1]+1){
            initPosition[1] = net-initPosition[1]-1;
        }else{
            initPosition[1] = boardSize[1]*2-net+initPosition[1];
        }
    }
    
    net = k%(boardSize[0]*2);
    
    if(initDirection[0]==1){
        if(net<boardSize[0]-initPosition[0]){
            initPosition[0] += net;
        }else if(net<boardSize[0]*2-initPosition[0]){
            initPosition[0] = 2*boardSize[0]-net-initPosition[0]-1;
        }else{
            initPosition[0] = initPosition[0]-(2*boardSize[0]-net);
        }
    }else{
        if(net<initPosition[0]+1){
            initPosition[0] -= net;
        }else if(net<boardSize[0]+initPosition[0]+1){
            initPosition[0] = net-initPosition[0]-1;
        }else{
            initPosition[0] = boardSize[0]*2-net+initPosition[0];
        }
    }    
    return initPosition;    
}
```

##### 첫 풀이 시도... 결국 안됨
```java
int[] chessBishopDream(int[] boardSize, int[] initPosition, int[] initDirection, int k) {
    
    for(int i=0; i<k%(boardSize[0]*2); i++){
        if(initDirection[0]==-1){
            if(initPosition[0]==0){
                initPosition[0]=0;
                initDirection[0]=1;
            }else{
                initPosition[0]--;
            }
            
        }else{
            if(initPosition[0]==boardSize[0]-1){
                initPosition[0]=boardSize[0]-1;
                initDirection[0]=-1;
            }else{
                initPosition[0]++;
            }
        }
    }
    
    for(int i=0; i<k%(boardSize[1]*2); i++){
        if(initDirection[1]==0){
            if(initPosition[1]==0){
                initPosition[1]=0;
                initDirection[1]=1;
            }else{
                initPosition[1]--;
            }
            
        }else{
            if(initPosition[1]==boardSize[1]-1){
                initPosition[1]=boardSize[1]-1;
                initDirection[1]=-1;
            }else{
                initPosition[1]++;
            }
        }
    }
    
    return initPosition;

}
```

##### 풀이 중 이게 있었다. 진짜 수학적이고 java 문법의 활용을 엄청 잘한 풀이이다.
```java
int[] chessBishopDream(int[] s, int[] p, int[] d, int k) {
    k %= (4 * s[0] * s[1]); //공배수
    for (int a = 0; a < k; a++)
        for (int i = 0; i < 2; i++)
            if ((p[i] += d[i]) < 0 || p[i] >= s[i])
                p[i] += (d[i] = -d[i]);
    
    return p;
}
```