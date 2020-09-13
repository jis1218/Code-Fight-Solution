디딤돌에 적힌 숫자가 순서대로 담긴 배열 stones와 한 번에 건너뛸 수 있는 디딤돌의 최대 칸수 k가 매개변수로 주어질 때, 최대 몇 명까지 징검다리를 건널 수 있는지 return 하도록 solution 함수를 완성해주세요.

[제한사항]
징검다리를 건너야 하는 니니즈 친구들의 수는 무제한 이라고 간주합니다.
stones 배열의 크기는 1 이상 200,000 이하입니다.
stones 배열 각 원소들의 값은 1 이상 200,000,000 이하인 자연수입니다.
k는 1 이상 stones의 길이 이하인 자연수입니다.
[입출력 예]
stones                      	k	result
[2, 4, 5, 3, 2, 1, 4, 2, 5, 1]	3	3

##### window sliding 이용한 경우
```java
import java.util.*;
class Solution {
    public int solution(int[] stones, int k) {
        int answer = 0;
        ArrayList<Integer> windowList = new ArrayList<>();
        int max_idx = 0;
        int max = 0;
        for(int i=0; i<=stones.length-k; i++){            
            if(max_idx<i || i==0){
                max = 0;
                for(int j=i; j<i+k; j++){
                    if(max<stones[j]){
                        max = stones[j];
                        max_idx = j;
                    }
                }
            }else{
                if(stones[i+k-1]>=max){
                    max = stones[i+k-1];
                    max_idx = i+k-1;
                }                
            }
            
            //System.out.println(max_idx);
            windowList.add(max);
        }
        int min = windowList.get(0);
        for(int i : windowList){
            if(i<min){
                min = i;
            }
        }
        
        return min;
    }
}
```

##### 잘 풀리나 한가지 문제점...
##### 예를 들어
```
[10, 9, 8, 7, 6....]
```
##### 일 경우 모든 경우를 다 탐색하므로 시간이 오래 걸린다.

##### 이분탐색으로 풀었다
```java
class Solution {
    public int solution(int[] stones, int k) {
        int answer = 0;
        int min = 200000000; int max = 0;
        for(int i : stones){
            min = Math.min(min, i);
            max = Math.max(max, i);
        }
        while(true){
            int mid = (min+max)/2;
            //System.out.println("min = " + min + ", max = " + max + ", mid = " + mid);

            boolean flag = true;
            int count = 0;
            for(int i : stones){
                if(mid>=i){
                    count++;
                }else{
                    count = 0;
                }
                if(count>=k){
                    max = mid;
                    flag = false;
                }
            }
            if(flag){
                min = mid+1;
            }
            if(max<=min) return max;
        }
    }
}
```