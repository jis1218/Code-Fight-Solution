```java
import java.util.regex.*;
class Solution {
  public String solution(String m, String[] musicinfos) {
      m = changeWord(m);      
      int real_len = m.length();
      int max_len = -1;
      int max_index = -1;
      for(int i=0; i<musicinfos.length; i++){
          String temp[] = musicinfos[i].split(",");
          int hour2 = Integer.valueOf(temp[1].split(":")[0]);
          int min2 = Integer.valueOf(temp[1].split(":")[1]);
          int hour1 = Integer.valueOf(temp[0].split(":")[0]);
          int min1 = Integer.valueOf(temp[0].split(":")[1]);
          
          int diff = hour2*60+min2 - (hour1*60+min1);
          
          temp[3] = changeWord(temp[3]);
          int music_len = temp[3].length();
          //System.out.println("len= " + music_len);
          //System.out.println("diff= " + diff);
          int remain = diff%music_len;   
          StringBuilder temp_str = new StringBuilder("");

          for(int j=0; j<diff/music_len; j++){
              temp_str.append(temp[3]);
              //System.out.println(temp_str);
          }
          temp_str.append(temp[3].substring(0, remain));
          System.out.println(temp_str.toString());
          Pattern p = Pattern.compile(m);
          Matcher mat = p.matcher(temp_str.toString());
          //boolean b = mat.find();
          //System.out.println(b);
          if(mat.find()){   
              System.out.println(diff);
              if(max_len<diff){
                  max_len = diff;
                  max_index = i;
              }
          }
          
      }
      
      return max_len==-1?"(None)":musicinfos[max_index].split(",")[2];
  }    
    public String changeWord(String s){
        return s.replace("A#", "a").replace("B#", "b").replace("C#", "c").replace("D#", "d").replace("E#", "e").replace("F#", "f").replace("G#", "g");
    }
}
```