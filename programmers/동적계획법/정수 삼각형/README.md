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