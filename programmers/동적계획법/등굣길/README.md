```java
class Solution {
    public int solution(int m, int n, int[][] puddles) {
        int answer = 0;
        int[][] memo = new int[m+1][n+1];
        return helper(m, n, puddles, memo);
    }
    
    public int helper(int m, int n, int[][] puddles, int[][] memo){
        if(m==1 && n==1) return 1;
        if(m<1 || n<1) return 0;
        if(isPuddle(m, n, puddles)) return 0;

        int first = memo[m-1][n]==0?helper(m-1, n, puddles, memo):memo[m-1][n];
        int second = memo[m][n-1]==0?helper(m, n-1, puddles, memo):memo[m][n-1];
        
        memo[m][n] = (first+second)%1000000007;
        return  memo[m][n];
    }
    
    public boolean isPuddle(int m, int n, int[][] puddles){
        for(int i=0; i<puddles.length; i++){
            if(puddles[i][0]==m && puddles[i][1]==n) return true;
        }
        return false;
    }
}
```