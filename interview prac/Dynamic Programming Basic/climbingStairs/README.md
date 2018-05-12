You are climbing a staircase that has n steps. You can take the steps either 1 or 2 at a time. Calculate how many distinct ways you can climb to the top of the staircase.
Example
For n = 1, the output should be
climbingStairs(n) = 1;
For n = 2, the output should be
climbingStairs(n) = 2.
You can either climb 2 steps at once or climb 1 step two times.
##### 재귀함수로 피보나치를 풀었다. 다른 풀이중에는 for문으로 푼 문제도 있다.
```java
int climbingStairs(int n) {
    if(n==1) return 1;
    if(n==2) return 2;
    
    return climbingStairs(n-2)+climbingStairs(n-1);    
}
```