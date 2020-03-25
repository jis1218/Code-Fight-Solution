You are supposed to label a bunch of boxes with numbers from 0 to n, and all the labels are stored in the array arr. Unfortunately one of the labels is missing. Your task is to find it.
Example
For arr = [3, 1, 0], the output should be
missingNumber(arr) = 2.

##### 나의 풀이
```java
int missingNumber(int[] arr) {
    Arrays.sort(arr);
    int num = 0;
    for(int i=0; i<arr.length; i++){
        if(num!=arr[i]) return num;
        
        num++;
    }
    
    return num;

}
```

##### 좋은 풀이
```java
int missingNumber(int[] arr) {
    int n = arr.length;
    int sum = n * (n + 1) / 2;
    for (int element : arr) {
        sum -= element;
    }
    return sum;
}
```

##### 다른 나의 풀이
```java
int missingNumber(int[] a) {
    int n = a.length, s=0;
    for(int i : a) s+=i;    
    return (n*n+n)/2-s;
}
```

##### 파이썬
```python
def missingNumber(a):
    l=len(a)
    return (l*l+l)/2-sum(a)
```