Given array of integers, for each position i, search among the previous positions for the last (from the left) position that contains a smaller value. Store this value at position i in the answer. If no such value can be found, store -1 instead.
Example
For items = [3, 5, 2, 4, 5], the output should be
arrayPreviousLess(items) = [-1, 3, -1, 2, 4].
```java
int[] arrayPreviousLess(int[] items) {
    int result[] = new int[items.length];
    result[0] = -1;
    for(int i=1; i<items.length; i++){
        for(int j=i-1; j>=0; j--){            
            if(items[i]>items[j]){
                result[i] = items[j];
                break;
            }else if(j==0){
                result[i] = -1;
            }            
        }
    }    
    return result;
}
```
##### O(1)을 안쓰고 푼 풀이
```java
int[] arrayPreviousLess(int[] items) {
    for (int i = items.length; i-->0; ){
        int best = -1;
        for (int j = 0; j < i; j++) {
            if (items[j] < items[i])
                best = items[j];
        }
        items[i] = best;
    }
    return items;
}
```