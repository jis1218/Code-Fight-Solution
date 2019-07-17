회사원 Demi는 가끔은 야근을 하는데요, 야근을 하면 야근 피로도가 쌓입니다. 야근 피로도는 야근을 시작한 시점에서 남은 일의 작업량을 제곱하여 더한 값입니다. Demi는 N시간 동안 야근 피로도를 최소화하도록 일할 겁니다.Demi가 1시간 동안 작업량 1만큼을 처리할 수 있다고 할 때, 퇴근까지 남은 N 시간과 각 일에 대한 작업량 works에 대해 야근 피로도를 최소화한 값을 리턴하는 함수 solution을 완성해주세요.
제한 사항
works는 길이 1 이상, 20,000 이하인 배열입니다.
works의 원소는 50000 이하인 자연수입니다.
n은 1,000,000 이하인 자연수입니다.
입출력 예
works
n
result
[4, 3, 3]
4
12
[2, 1, 2]
1
6
[1,1]
3
0

##### 문제 접근 방법은 찾았음, 코드도 훨씬 간결
```java
import java.util.*;
class Solution {
    public long solution(int n, int[] works) {
        long answer = 0;
        works = Arrays.stream(works).boxed().sorted(Comparator.reverseOrder()).mapToInt(i->i).toArray();
        int count = 1;
        for(int i = 0; i<works.length-1; i++){
            int sub = works[i]-works[i+1];
            for(int j=0; j<i+1; j++){
                works[j]-=Math.min(sub,n);                
                n-=Math.min(sub,n);
                if(n==0) break;
            }
        }
        
        if(n==0){
            for(int i=0; i<works.length; i++){
            answer+=(long)works[i]*(long)works[i];                
            }
            return answer;
        }else{
            long a = works[0]-n/works.length;
            if(a<1) return 0;
            return a*a*(works.length-n%works.length) + (a-1)*(a-1)*(n%works.length);
        }
    }
}
```

##### 문제 접근 방법이 완전 틀림... 가령 10, 9가 있고 n=8이라고 하면 나는 가장 큰수에서 그냥 8을 빼버렸지만 그렇게 하면 안됨
##### 평균으로 접근해야 할듯...
```java
import java.util.*;
class Solution {
    public long solution(int n, int[] works) {
        long answer = 0;
        works = Arrays.stream(works).boxed().sorted(Comparator.reverseOrder()).mapToInt(i->i).toArray();
        int min = works[works.length-1];
        
        for(int i=0; i<works.length; i++){
            int diff = works[i]-min;
            if(diff==0) break;
            if(n>=diff){
                n -= diff;
                works[i] = min;
            }else{
                works[i] -= n;
                break;
            }
        }
        long sum = 0;
        int stop = 0;
        if(n==0){
            works = Arrays.stream(works).boxed().sorted(Comparator.reverseOrder()).mapToInt(i->i).toArray();
            for(int i=0; i<works.length; i++){
                // if(works[i]==min){
                //     stop = i;
                //     break;
                // }
                sum += works[i]*works[i];
            }
            //return sum + (long)(((long)works.length-(long)stop)*(long)min*(long)min);
            return sum;
        }        
        int temp = (int)Math.ceil((double)n/works.length);

        if(min-temp<0) return 0;
        return (long)n*((long)min-(long)temp)*((long)min-(long)temp)+(long)((long)works.length-(long)n)*((long)min-(long)temp+1)*((long)min-(long)temp+1);
    
    }
}
```