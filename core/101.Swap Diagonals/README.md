The longest diagonals of a square matrix are defined as follows:
the first longest diagonal goes from the top left corner to the bottom right one;
the second longest diagonal goes from the top right corner to the bottom left one.
Given a square matrix, your task is to swap its longest diagonals by exchanging their elements at the corresponding positions.
```java
int[][] swapDiagonals(int[][] matrix) {
    int len = matrix.length-1;
    for(int i=0; i<matrix.length/2; i++){
        int temp = matrix[i][i];
        matrix[i][i] = matrix[i][len-i];
        matrix[i][len-i] = temp;
        temp = matrix[len-i][i];
        matrix[len-i][i] = matrix[len-i][len-i];
        matrix[len-i][len-i] = temp;
    }
    
    return matrix;
}
```