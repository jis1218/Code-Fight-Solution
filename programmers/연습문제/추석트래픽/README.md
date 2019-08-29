```java
import java.util.*;
class Solution {
  public int solution(String[] lines) {
      int answer = 0;
      long[] front = new long[lines.length];
      long[] back = new long[lines.length];
      for(int i=0; i<lines.length; i++){
          String[] temp = lines[i].split(" ");
        String time[] = temp[1].split(":");
          double time_double = Double.valueOf(time[2]);
          time_double *= 1000;
          int time_int = (int) time_double;
          String term = temp[2].substring(0, temp[2].length()-1);
          double term_double = Double.valueOf(term);
          term_double *= 1000;
          int fro = (int)term_double;
          //System.out.println("fro = " + fro + ", time = " + time_int);
        long result = Long.valueOf(time[0])*3600000+Long.valueOf(time[1])*60000+time_int;
          back[i] = result;
          front[i] = result-fro+1;
      }
      
      Arrays.sort(front);
      int max=0;
      for(int i=0; i<front.length; i++){
          int count = 0;
          for(int j=0; j<back.length; j++){
              if((front[i]-999<=back[j] && back[j]<=front[i]) 
                 || front[j]<=front[i] && front[j]>=front[i]-999                  
                || (front[i]>=front[j] && front[i]<=back[j])){
                  count++;
              }
          }
          if(count>max){
              max = count;
          }
      }
      for(int i=0; i<back.length; i++){
          int count2 = 0;
          for(int j=0; j<front.length; j++){
              if((back[i]+999>=front[j] && front[j]>=back[i]) 
                 || (front[j]>=front[i] && front[j]<=front[i]+999)                 
                ||(back[i]<=back[j] && back[i]>=front[j])){
                  count2++;
              }
          }
          if(count2>max){
              max = count2;
          }
      }
      return max;
  }   
}
```