```python
def extractEachKth(inputArray, k):
    return [inputArray[i] for i in range(len(inputArray)) if i%k is not k-1]
```

##### 다른 풀이
```python
def extractEachKth(inputArray, k):
    del inputArray[k-1::k]
    return inputArray
```

##### 2년전 java 풀이
```java
int[] extractEachKth(int[] inputArray, int k) {
    ArrayList<Integer> list = new ArrayList<>();
    for(int i=0; i<inputArray.length; i++){
        if(((i+1)%k)!=0){
        list.add(inputArray[i]);
        }
    }
    
    int result[] = new int[list.size()];
    for(int i=0; i<list.size(); i++){
        result[i] = list.get(i).intValue();
    }
    return result;
}
```