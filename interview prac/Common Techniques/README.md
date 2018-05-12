Given an array of integers, write a function that determines whether the array contains any duplicates. Your function should return true if any element appears at least twice in the array, and it should return false if every element is distinct.
Example
For a = [1, 2, 3, 1], the output should be
containsDuplicates(a) = true.
There are two 1s in the given array.
For a = [3, 1], the output should be
containsDuplicates(a) = false.
The given array contains no duplicates.

##### Set으로 풀어보았다. 다른 풀이들을 보니 Set을 이용하거나 Sorting을 이용하여 풀었따. 코드파이트 자체에서는 다음과 같은 힌트를 준다. There are many different approaches to this problem. The simplest one uses a hash table or a hash set.
```java
boolean containsDuplicates(int[] a) {
    Set<Integer> set = new HashSet<>();
    for(int i : a) set.add(i);
    
    if(set.size()!=a.length) return true;
    
    return false;
}
```

##### Quick Sort를 구현하여 풀어보았다. 시간 초과 에러 뜸

```java
boolean containsDuplicates(int[] a) {
    quickSort(a, 0, a.length-1);
    
    for(int i=0; i<a.length-1; i++){
        if(a[i]==a[i+1]) return true;
    }
    
    return false;
    
}

int partition(int[] a, int start, int end){
    int unknownStart = start;
    int greaterStart = start;
    
    while(end>unknownStart){
        if(a[end]>a[unknownStart]){
            int temp = a[unknownStart];
            a[unknownStart] = a[greaterStart];
            a[greaterStart] = temp;
            unknownStart++;
            greaterStart++;
        }else{
            unknownStart++;
        }
    }
    
    int temp = a[end];
    a[end] = a[greaterStart];
    a[greaterStart] = temp;  
    
    return greaterStart;
    
}

void quickSort(int[] a, int p, int r){
    if(r-p>0){
        int part = partition(a, p, r);
        quickSort(a, p, part-1);
        quickSort(a, part+1, r);
    }
}
```