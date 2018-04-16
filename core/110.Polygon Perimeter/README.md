You have a rectangular white board with some black cells. The black cells create a connected black figure, i.e. it is possible to get from any black cell to any other one through connected adjacent (sharing a common side) black cells.
Find the perimeter of the black figure assuming that a single cell has unit length.
It's guaranteed that there is at least one black cell on the table.
Example
For
matrix = [[false, true,  true ],
          [true,  true,  false],
          [true,  false, false]]

##### 나의 풀이

```java
int polygonPerimeter(boolean[][] matrix) {
    int cnt=0;
    
    for(int i=0; i<matrix.length; i++){
        for(int j=0; j<matrix[0].length; j++){
            
            if(matrix[i][j]){
                if(i-1>=0){
                    if(!matrix[i-1][j]) cnt++;  
                }else{
                    cnt++;
                }
                
                if(i+1<matrix.length){
                    if(!matrix[i+1][j]) cnt++; 
                }else{
                    cnt++;
                }
                
                if(j-1>=0){
                    if(!matrix[i][j-1]) cnt++;
                }else{
                    cnt++;
                }
                
                if(j+1<matrix[0].length){
                    if(!matrix[i][j+1]) cnt++;
                }else{
                    cnt++;
                }                
            }   
        }
    }    
    return cnt;
}
```
##### 다른 사람의 풀이... 이게 무슨 풀이인가??
```java
int x, y, s, p;
int polygonPerimeter(boolean[][] m) {
    for (boolean[] a:m){
        p = x = 0;
        for (boolean b:a){
            s += b?
                (y>0 && m[y-1][x]?2:4)
                    - p
                :0;
            p = b?2:0;
            x++;
        }
        
        ++y;
    }
    return s;
}
```