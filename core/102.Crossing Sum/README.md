Given a rectangular matrix and integers a and b, consider the union of the ath row and the bth (both 0-based) column of the matrix (i.e. all cells that belong either to the ath row or to the bth column, or to both). Return sum of all elements of that union.
```java
int crossingSum(int[][] matrix, int a, int b) {
    int sum = 0;
    for(int i=0; i<matrix[0].length; i++){
        sum += matrix[a][i];
    }
    for(int j = 0; j<matrix.length; j++){
        sum += matrix[j][b];
    }
    return sum - matrix[a][b];
}
```