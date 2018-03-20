The longest diagonals of a square matrix are defined as follows:
the first longest diagonal goes from the top left corner to the bottom right one;
the second longest diagonal goes from the top right corner to the bottom left one.
Given a square matrix, your task is to reverse the order of elements on both of its longest diagonals.
```java
int[][] reverseOnDiagonals(int[][] matrix) {
    int len = matrix.length;
    
    for(int i=0; i<(len+1)/2; i++){
        int temp = matrix[i][i];
        matrix[i][i] = matrix[len-1-i][len-1-i];
        matrix[len-1-i][len-1-i] = temp;
        
        temp = matrix[len-1-i][i];
        matrix[len-1-i][i] = matrix[i][len-1-i];
        matrix[i][len-1-i] = temp;
    }
    
    return matrix;

}
```