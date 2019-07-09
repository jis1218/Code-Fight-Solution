가로 길이가 2이고 세로의 길이가 1인 직사각형모양의 타일이 있습니다. 이 직사각형 타일을 이용하여 세로의 길이가 2이고 가로의 길이가 n인 바닥을 가득 채우려고 합니다. 타일을 채울 때는 다음과 같이 2가지 방법이 있습니다.

타일을 가로로 배치 하는 경우
타일을 세로로 배치 하는 경우
##### 비슷한 문제를 풀어봐서 쉽게 풀었음
```java
class Solution {
  public int solution(int n) {
      long a = 1;
      if(n==1) return 1;
      long b = 2;

      for(int i=0; i<n-2; i++){
          long temp = b;
          b = (a+b)%1000000007;
          a = temp;
      }      
      return (int)(b%1000000007);
  }
}
```