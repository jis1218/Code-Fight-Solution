Two two-dimensional arrays are isomorphic if they have the same number of rows and each pair of respective rows contains the same number of elements.
Given two two-dimensional arrays, check if they are isomorphic.
```java
boolean areIsomorphic(int[][] array1, int[][] array2) {

    if(array1.length != array2.length) return false;
    for(int i=0; i<array1.length; i++){
        if(array1[i].length!=array2[i].length) return false;
    }
    
    return true;
}
```

```python
def areIsomorphic(array1, array2):
    if(len(array1)!=len(array2)):
        return False
    for i in range(len(array1)):
        if(len(array1[i])!=len(array2[i])):
           return False
    return True
```

##### 더 좋은 풀이
```python
def areIsomorphic(array1, array2):
    return list(map(len,array1)) == list(map(len,array2))
```