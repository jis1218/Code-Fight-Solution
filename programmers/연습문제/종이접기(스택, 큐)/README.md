```java
import java.util.*;
class Solution {
  public int[] solution(int n) {
      int[] answer = {};
      ArrayList<Integer> answerList = new ArrayList<>();
      LinkedList<Integer> list = new LinkedList<>();
      list.add(0);
      int cnt = 1;
      while(cnt<n){
          LinkedList<Integer> temp_list = new LinkedList<>();
          int toggle = 0;
          while(list.size()!=0){
              temp_list.add(toggle);
              temp_list.add(list.pollFirst());
              if(toggle==0){
                  toggle = 1;
              }else{
                  toggle = 0;
              }
          }
          temp_list.add(1);
          list = temp_list;
          cnt++;
      }
      Integer intArray[] = list.toArray(new Integer[]{});
//       while(iter.hasNext()){
//           int i = iter.next();
//           answerList.add(0, i);    이렇게 하니까 시간이 엄청 늘어남
//           //System.out.println(i);
          
//       }
      return Arrays.stream(intArray).mapToInt(i->i).toArray();
  }
}
```