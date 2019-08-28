```java
import java.util.*;
class Solution {
  public int solution(String[] words) {
      int answer = 0;
      Arrays.sort(words);
      int prev = 0;
      for(int i=0; i<words.length-1; i++){
          int temp = 0;
          for(int j=0; j<=Math.min(words[i].length(), words[i+1].length()); j++){
              if(Math.min(words[i].length(), words[i+1].length())>j &&
                 words[i].charAt(j)==words[i+1].charAt(j)){
                  temp++;
              }else{ 
                  if(temp<=prev){
                      answer += prev+1;
                      prev = temp;
                  }else{
                      if(j<Math.min(words[i].length(), words[i+1].length())){
                          answer += temp+1;
                      }else{
                          answer += temp;
                      }                      
                      prev = temp;    
                  }                  
                  break;
              }
          }
      }      
      return answer + prev + 1;
  }
}
```