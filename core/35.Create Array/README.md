Given an integer size, return array of length size filled with 1s.
Example
For size = 4, the output should be
createArray(size) = [1, 1, 1, 1].
```java
int[] createArray(int size) {
    int []result = new int[size];
    for(int i=0; i<size; i++){
        result[i]=1;
    }
    return result;

}
```