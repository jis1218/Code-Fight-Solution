Given integers n, l and r, find the number of ways to represent n as a sum of two integers A and B such that l ≤ A ≤ B ≤ r.
Example
For n = 6, l = 2 and r = 4, the output should be
countSumOfTwoRepresentations2(n, l, r) = 2.
There are just two ways to write 6 as A + B, where 2 ≤ A ≤ B ≤ 4: 6 = 2 + 4 and 6 = 3 + 3.
```java
int countSumOfTwoRepresentations2(int n, int l, int r) {
    int result=0;
    for(int i=l; i<=r; i++){
        if(n-i<=r && n-i>=l){
            result++;
        }
    }
    return result%2==1?result/2+1:result/2;
}
```

##### 다른 풀이
```java
int countSumOfTwoRepresentations2(int n, int l, int r) {
    return Math.max(n/2+1-Math.max(l, Math.max(n-r,0)),0);
        
}
```

##### 또 다른 풀이
```java
int countSumOfTwoRepresentations2(int n, int l, int r) {
    int t = 0;
    for (int i = l; i <= r; i++) {
        if (n-i >= i && n-i <= r)
            t++;
    }
    return t;
}
```
