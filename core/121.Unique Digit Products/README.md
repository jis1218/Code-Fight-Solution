Let's call product(x) the product of x's digits. Given an array of integers a, calculate product(x) for each x in a, and return the number of distinct results you get.
Example
For a = [2, 8, 121, 42, 222, 23], the output should be
uniqueDigitProducts(a) = 3.
Here are the products of the array's elements:
2: product(2) = 2;
8: product(8) = 8;
121: product(121) = 1 * 2 * 1 = 2;
42: product(42) = 4 * 2 = 8;
222: product(222) = 2 * 2 * 2 = 8;
23: product(23) = 2 * 3 = 6.
As you can see, there are only 3 different products: 2, 6 and 8.

##### 나의 풀이
```java
int uniqueDigitProducts(int[] a) {
    
    HashSet<Integer> set = new HashSet<>();
    
    for(int i: a){
        int time = 1;
        while(i>0){
            time *= i%10;
            i /= 10;
        }
        set.add(time);
    }
    
    return set.size();
}
```

##### Set을 안쓰고 풀이
```java
int uniqueDigitProducts(int[] a) {
    for (int i = 0 ; i  < a.length; i++) 
        a[i] = prod(a[i]);
    Arrays.sort(a);
    int count = 1;
    for (int i = 1; i < a.length; i++)
        if (a[i] != a[i-1])
            count++;
    return count;
}

int prod (int a) {
    int value = 1;
    while (a > 0) {
        value *= a%10;
        a /= 10;
    }
    return value;
}
```