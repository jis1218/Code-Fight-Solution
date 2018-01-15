
##### 최종 풀이... 잘 안되었던 부분은 for문이 두개다 보니 시간이 많이 걸린다는 점... 그것을 memory를 이용하여 해결하였는데 문제는 소수점이었다. double로 안해주니 계속 int로 인식하여 m과 n이 커질 경우 오차가 생긴다는 것이었다.
```java
int countBlackCells(int n, int m) {
    int result = 0;
    int memory = 0;

    for(int i=0; i<n; i++){
        int index =0;
        for(int j=memory; j<m; j++){       
            // 첫번째 경우
            if((i+1)*(double)m/n>=j && (i+1)*(double)m/n<=j+1){
                result++;
            // 두번째 경우
            }else if((j+1)*(double)n/m>=i && (j+1)*(double)n/m<=i+1){
                result++;
                index++;
            // 다 찾은 경우
            }else if(index>0){
                memory = j-2;
                break;
            }   
        }
    }
    return result;
}
```java

##### 좋은 풀이 - 최대 공약수를 이용하였다. 왜 최대공약수를 이용하여 풀이를 했는지 알수가 없다. 공부 필요
```java
int countBlackCells(int n, int m) {
    int max = 1;
    for (int k = 1; k <= n; k++) {
        if (n%k == 0 && m%k == 0)
            max = k;
    }
    return n+m+max-2;
}
```
```java
int countBlackCells(int n, int m) {
    return n + m + GCD(n, m) - 2;
}

int GCD(int a, int b) { return b==0 ? a : GCD(b, a%b); }
```
