Let's call two integers A and B friends if each integer from the array divisors is either a divisor of both A and B or neither A nor B. If two integers are friends, they are said to be in the same clan. How many clans are the integers from 1 to k, inclusive, broken into?
Example
For divisors = [2, 3] and k = 6, the output should be
numberOfClans(divisors, k) = 4.
The numbers 1 and 5 are friends and form a clan, 2 and 4 are friends and form a clan, and 3 and 6 do not have friends and each is a clan by itself. So the numbers 1 through 6 are broken into 4 clans.

```java
int numberOfClans(int[] divisors, int k) {
    
    Set<String> set = new TreeSet<>();
    
    for(int i=1; i<=k; i++){
        String str = "";
        for(int j : divisors){
            if(i%j==0){
                str += j;
            }
        }
        set.add(str);
    }    
    return set.size();
}
```

##### TreeSet을 사용하지 않은 풀이
```java
int numberOfClans(int[] divisors, int k) {
    int t = 0;
    for (int i = 1; i <= k; i++) {
        boolean alone = true;
        for (int j = 1; j < i; j++) {
            boolean paired = true;
            for (int l : divisors) {
                if ((i%l == 0 && j%l != 0) || (i%l!= 0 && j%l == 0))
                    paired = false;
            }
            if (paired)
                alone = false;
        }
        if (alone)
            t++;
    }
    return t;
}
```