N candles are placed in a row, some of them are initially lit. For each candle from the 1st to the Nth the following algorithm is applied: if the observed candle is lit then states of this candle and all candles before it are changed to the opposite. Which candles will remain lit after applying the algorithm to all candles in the order they are placed in the line?
Example
For a = [1, 1, 1, 1, 1], the output should be
switchLights(a) = [0, 1, 0, 1, 0].
```java
int[] switchLights(int[] a) {
    
    int res[] = new int[a.length];
    
    for(int i=0; i<res.length; i++){
        int sum = 0;
        for(int j=i; j<res.length; j++){
             sum += a[j];
        }
        res[i] = (sum+a[i])%2;
    }    
    return res;
}
```

##### 다른 풀이
```java
int[] switchLights(int[] a) {
    for (int i = 0; i < a.length; i++) {
        for (int j = 0; j <= i; j++) {
            if (a[i] == 1)
                a[j] ^= 1;
        }
    }
    return a;
}
```
