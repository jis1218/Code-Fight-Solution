```java
class Solution {
  int MOD = 20170805;
  public int solution(int m, int n, int[][] cityMap) {
      int memo[][] = new int[m][n];
      for(int i=0; i<m; i++){
          for(int j=0; j<n; j++){
              memo[i][j] = -1;
          }
      }
      int a = helper(cityMap, memo, m-2, n-1, true);
      int b = helper(cityMap, memo, m-1, n-2, false);       
      return (a + b) % MOD;
  }
    public int helper(int[][] cityMap, int[][] memo, int m, int n, boolean flow){
        if(m<0 || n<0 || cityMap[m][n]==1 ) return 0;
        if(m==0 && n==0) return 1;
        if(cityMap[m][n]==2){
            if(flow) return helper(cityMap, memo, m-1, n, true);
            else return helper(cityMap, memo, m, n-1, false);
        }
        if(memo[m][n]!=-1) return memo[m][n] % MOD;
        memo[m][n] = helper(cityMap, memo, m-1, n, true) + 
                      helper(cityMap, memo, m, n-1, false);
        return memo[m][n] % MOD;
    }
}
```