Given a rectangular matrix and an integer column, return an array containing the elements of the columnth column of the given matrix (the leftmost column is the 0th one).

```java
int[] extractMatrixColumn(int[][] matrix, int column) {
    int[] result = new int[matrix.length];
    for(int i=0; i<matrix.length; i++){
        result[i] = matrix[i][column];
    }
    return result;
}
```

```python
def extractMatrixColumn(matrix, column):
    a = [];
    for i in range(len(matrix)):
        a.append(matrix[i][column])
        
    return a
```

##### Python 다른 좋은 풀이
```python
def extractMatrixColumn(matrix, column):
    return [x[column] for x in matrix] # x in matrix라 함은 matrix[0], matrix[1]을 말함, 그러므로 x[column]은 matrix][0][column], matrix[1][column] 이다.
```