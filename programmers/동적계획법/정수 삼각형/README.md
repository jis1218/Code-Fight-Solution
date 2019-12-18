##### 정수 삼각형 문제...
##### 단순히 재귀함수를 쓰게 되면 시간 초과가 뜬다
##### 동적계획법을 알아야 풀 수 있는 문제
```java
class Solution {
    int max = 0;
    public int solution(int[][] triangle) {
        int[][] memoization = new int[triangle.length][triangle[0].length];
        sumNext(0, 0, triangle, 0, memoization);
        
        return max;
    }
    
    public void sumNext(int fidx, int sidx, int [][]triangle, int sum, int[][] memoization){
        if(fidx==triangle.length-1){
            if(max<sum+triangle[fidx][sidx]){
                max = sum+triangle[fidx][sidx];
            }
            return;
        }
        sum += triangle[fidx][sidx];
        sumNext(fidx+1, sidx, triangle, sum);
        sumNext(fidx+1, sidx+1, triangle, sum);
    }
}
```
##### 위의 코드에서 동적계획법을 추가하면 아래와 같다.
##### 하지만 역시나 효율성은 떨어진다. 이 코드는 DFS이기 때문이다.
```java
class Solution {
    int temp[][];
    int max = 0;
    public int solution(int[][] triangle) {
        int[][] memoization = new int[triangle.length][triangle[0].length];
        sumNext(0, 0, triangle, 0, memoization);
        temp = new int[triangle.length][triangle.length];
        
        return max;
    }
    
    public void sumNext(int fidx, int sidx, int [][]triangle, int sum, int[][] memoization){
        if(fidx==triangle.length-1){
            if(max<sum+triangle[fidx][sidx]){
                max = sum+triangle[fidx][sidx];
            }
            return;
        }
        sum += triangle[fidx][sidx];
        if(temp[fidx][sidx]<sum){
            temp[fidx][sidx] = sum;
            sumNext(fidx+1, sidx, triangle, sum);
            sumNext(fidx+1, sidx+1, triangle, sum);
        }
        
    }
}
```

##### 결국 BFS + 동적계획법을 이용해야한다.
```java
import java.util.*;
class Solution {
    public int solution(int[][] triangle) {
        int max = 0;
        int[][] temp = new int[triangle.length][triangle.length];
        temp[0][0] = triangle[0][0];
        for(int i=1; i<triangle.length; i++){
            for(int j=0; j<triangle[i].length; j++){
                if(j<triangle[i-1].length && j-1>=0){
                    temp[i][j] = Math.max(temp[i-1][j-1], temp[i-1][j]) + triangle[i][j];
                }else if(j-1<0){
                    temp[i][j] = temp[i-1][j] + triangle[i][j];
                }else{
                    temp[i][j] = temp[i-1][j-1] + triangle[i][j];
                }
            }
        }
        
        for(int i : temp[temp.length-1]){
            if(i>max) max = i;
        }
        
        return max;
    }    
}
```