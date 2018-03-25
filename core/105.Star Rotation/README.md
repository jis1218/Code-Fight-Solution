Consider a (2k+1) × (2k+1) square subarray of an integer integers matrix. Let's call the union of the square's two longest diagonals, middle column and middle row a star. Given the coordinates of the star's center in the matrix and its width, rotate it 45 · t degrees clockwise preserving position of all matrix elements that do not belong to the star.
```java
int[][] starRotation(int[][] matrix, int width, int[] center, int t) {

    int a = center[0];
    int b = center[1];
    for(int j=0; j<t%8; j++){
        for(int i=1; i<=width/2; i++){
        int temp = matrix[a-i][b];
        matrix[a-i][b] = matrix[a-i][b-i];
        matrix[a-i][b-i] = matrix[a][b-i];
        matrix[a][b-i] = matrix[a+i][b-i];
        matrix[a+i][b-i] = matrix[a+i][b];
        matrix[a+i][b] = matrix[a+i][b+i];
        matrix[a+i][b+i] = matrix[a][b+i];
        matrix[a][b+i] = matrix[a-i][b+i];
        matrix[a-i][b+i] = temp;        
        }
    }
    
    
    return matrix;
}
```