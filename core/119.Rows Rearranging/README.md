Given a rectangular matrix of integers, check if it is possible to rearrange its rows in such a way that all its columns become strictly increasing sequences (read from top to bottom).
Example
For
matrix = [[2, 7, 1], 
          [0, 2, 0], 
          [1, 3, 1]]
the output should be
rowsRearranging(matrix) = false;
For
matrix = [[6, 4], 
          [2, 2], 
          [4, 3]]
the output should be
rowsRearranging(matrix) = true.

##### 나의 풀이... O(N^2) 인가???
```java
boolean rowsRearranging(int[][] matrix) {
    int len = matrix[0].length;
    for(int i=0; i<matrix.length-1; i++){
        for(int j=i+1; j<matrix.length; j++){
            if(matrix[i][0]>matrix[j][0]){
                int temp[] = Arrays.copyOf(matrix[i], len);
                matrix[i] = Arrays.copyOf(matrix[j], len);
                matrix[j] = Arrays.copyOf(temp, len);
            }
        }
    }
    
    for(int i=0; i<matrix.length-1; i++){
        for(int j=0; j<len; j++){
            if(matrix[i][j]>=matrix[i+1][j]){
                return false;
            }
        }
    }
    return true;
}
```

##### 내가 원했던 풀이다. 잘 풀었다. O(N^3) 이지만 배열을 복사하는 과정이 없기 때문에 더 빠를 것 같다
```java
boolean rowsRearranging(int[][] matrix) {
    for (int i = 1; i < matrix.length; i++) {
        for (int j = 0; j < i; j++) {
            for (int k = 0; k < matrix[0].length; k++) {
                if (matrix[i][k] == matrix[j][k])
                    return false;
                if (matrix[i][0]<matrix[j][0] ^ matrix[i][k]<matrix[j][k]) 
                    return false;
            }
        }
    }
    return true;
}
```