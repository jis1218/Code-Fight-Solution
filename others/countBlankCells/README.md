Imagine a white rectangular grid of n rows and m columns divided into two parts by a diagonal line running from the upper left to the lower right corner. Now let's paint the grid in two colors according to the following rules:

A cell is painted black if it has at least one point in common with the diagonal;
Otherwise, a cell is painted white.
Count the number of cells painted black.
```java
int countBlackCells(int n, int m) {    
    if(m>n){
        int temp = n;
        n = m;
        m = temp;
    }
    int q = n;
    int r = m;
    int gcd = r;
    while(true){
        int remain = q%r;
        if(remain==0){
            gcd = r;
            break;
        }
        q = r;
        r = remain;
    }

    n/=r;
    m/=r;

    HashSet<String> set = new HashSet<>();
    for(int i=0; i<n; i++){
        if(i*m%n==0){
            set.add(i + "," + i*m/n);
            if(i-1>=0) set.add(i-1 + "," + i*m/n);
            if(i-1>=0 && (i-1)*m/n-1>=0) set.add(i-1 + "," + String.valueOf((i-1)*m/n-1));
            if(i*m/n-1>=0) set.add(i + "," + String.valueOf(i*m/n-1));
        }else{
            set.add(i + "," + i*m/n);
            set.add(i-1 + "," + i*m/n);
        }
    }
    n-=1;
    m-=1;
    set.add(n + "," + m);

    return set.size()*r + (r-1)*2;

}
```

##### 나의 풀이는 무식한 풀이...
##### 다른 수학적 풀이
```java
int countBlackCells(int n, int m) {
    int r = n + m - 2, t;
    while (m > 0) {
        t = n;
        n = m;
        m = t % m;
    }
    return r + n;
}

```
