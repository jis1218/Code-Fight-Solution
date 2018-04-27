Given an array of integers, sort its elements by the difference of their largest and smallest digits. In the case of a tie, that with the larger index in the array should come first.
Example
For a = [152, 23, 7, 887, 243], the output should be
digitDifferenceSort(a) = [7, 887, 23, 243, 152].
Here are the differences of all the numbers:
152: difference = 5 - 1 = 4;
23: difference = 3 - 2 = 1;
7: difference = 7 - 7 = 0;
887: difference = 8 - 7 = 1;
243: difference = 4 - 2 = 2.
23 and 887 have the same difference, but 887 goes after 23 in a, so in the sorted array it comes first.
```java
int[] digitDifferenceSort(int[] a) {
    int []diff = new int[a.length];
    for(int i=0; i<a.length; i++){
        diff[i] = getDiff(a[i]);
    }
    
    for(int i=0; i<a.length-1; i++){
        for(int j=i+1; j<a.length; j++){
            if(diff[i]>=diff[j]){
                int temp = a[i];
                a[i] = a[j];
                a[j] = temp;
                int temp2 = diff[i];
                diff[i] = diff[j];
                diff[j] = temp2;
            }
        }
    }
    
    return a;
}

int getDiff(int a){
    int max = a%10;
    int min = a;
    while(a>0){
        min = Math.min(a%10, min);
        max = Math.max(a%10, max);
        a /= 10;
    }
    return max-min;
}
```

##### 다른 풀이 - 연구해보자
```java
int[] digitDifferenceSort(int[] a) {
    long[] b = new long[a.length];
    for (int i = 0; i < a.length; i++){
        long max = 0, min = 9;
        for (int v = a[i]; v > 0; v/=10){
            max = Math.max(max, v%10);
            min = Math.min(min, v%10);
        }
        b[i] = ((max-min) << 36) + ((10000l - i) << 20) + a[i]; 
    }
    
    Arrays.sort(b);
    for (int i = 0; i < a.length; i++){
        a[i] = (int)(b[i] & ((1<<20)-1));
    }
    return a;
}
```