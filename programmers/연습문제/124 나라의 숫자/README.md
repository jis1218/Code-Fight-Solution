124 나라가 있습니다. 124 나라에서는 10진법이 아닌 다음과 같은 자신들만의 규칙으로 수를 표현합니다.

124 나라에는 자연수만 존재합니다.
124 나라에는 모든 수를 표현할 때 1, 2, 4만 사용합니다.
예를 들어서 124 나라에서 사용하는 숫자는 다음과 같이 변환됩니다.

10진법	124 나라	10진법	124 나라
1	1	6	14
2	2	7	21
3	4	8	22
4	11	9	24
5	12	10	41
자연수 n이 매개변수로 주어질 때, n을 124 나라에서 사용하는 숫자로 바꾼 값을 return 하도록 solution 함수를 완성해 주세요.

제한사항

##### 최악의 풀이...

```java
class Solution {
  public String solution(int n) {
      String result = "";
      int remain = 0;
      while(n!=0){
          remain = n%3;
          result += remain;
          n = n/3;
      }
      StringBuilder builder = new StringBuilder(result);
      boolean flag = false;
      for(int i=0; i<result.length(); i++){
          if(flag){
              if(builder.charAt(i)=='0'){
                  builder.replace(i, i+1, "2");
                  flag = true;
              }else{
                  builder.replace(i, i+1, String.valueOf(builder.charAt(i)-'1'));
                  if(builder.charAt(i)=='0' && i!=result.length()-1){
                      builder.replace(i, i+1, "4");
                    flag = true;
                  }else{
                        flag = false;
                  }
              }
              
          }else{
             if(builder.charAt(i)=='0'){
              builder.replace(i, i+1, "4");
              flag = true;   
            }else{
                 flag = false;
             } 
          }
          
      }
      builder.reverse();
      if(builder.charAt(0)=='0') builder.deleteCharAt(0);
      return builder.toString();
  }
}
```

##### 충분히 쉽게 풀 수 있음
```java
class Solution {
  public String solution(int n) {
      String[] num = {"4","1","2"};
      String answer = "";

      while(n > 0){
          answer = num[n % 3] + answer;
          n = (n - 1) / 3;
      }
      return answer;
  }
}
```