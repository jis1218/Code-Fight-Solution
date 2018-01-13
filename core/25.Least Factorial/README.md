Given an integer n, find the minimal k such that
k = m! (where m! = 1 * 2 * ... * m) for some integer m;
k >= n.
In other words, find the smallest factorial which is not less than n.
Example
For n = 17, the output should be
leastFactorial(n) = 24.
17 < 24 = 4! = 1 * 2 * 3 * 4, while 3! = 1 * 2 * 3 = 6 < 17).
##### 나의 풀이
```java
int leastFactorial(int n) {
    int fac = 1;
    int sum = 1;
    while(true){
        sum *= fac;
        fac++;

        if(sum>=n){
            return sum;
        }
    }
}
```

##### 이런 풀이도 있다.
```java
int leastFactorial(int n) {
    int k = 1, c = 1;
    while (k < n) k *= c++;
    return k;
}
```
