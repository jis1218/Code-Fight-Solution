```java
import java.util.*;
class Solution {
  public int[] solution(int m, int n, int[][] picture) {
      boolean[][] memo = new boolean[m][n];
      ArrayList<Integer> list = new ArrayList<>();
      
      for(int i=0; i<m; i++){
          for(int j=0; j<n; j++){
              if(picture[i][j]!=0 && !memo[i][j]){
                  //System.out.println("Start = " + i + ", " + j);
                  list.add(helper(i, j, picture, memo, picture[i][j]));                  
              }else{
                  memo[i][j]=true;
              }              
          }
      }
      int max=0;
      for(int i : list) if(i>max) max=i;      
      int[] answer = new int[2];
      answer[0] = list.size();
      answer[1] = max;
      //System.out.println(answer[0]);
      //System.out.println(answer[1]);
      return answer;
  }   
    
    public int helper(int m, int n, int[][] picture, boolean[][] memo, int num){
        if(m<0 || n<0 || m>=picture.length || n>=picture[0].length || picture[m][n]!=num || memo[m][n]) return 0;        
        memo[m][n]=true;
        //System.out.println("jjak = " + m + ", " + n);
        return 1 + helper(m, n-1, picture, memo, num) 
            + helper(m, n+1, picture, memo, num) 
            + helper(m+1, n, picture, memo, num) 
            + helper(m-1, n, picture, memo, num);
    }   
}
```