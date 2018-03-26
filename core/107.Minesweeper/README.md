In the popular Minesweeper game you have a board with some mines and those cells that don't contain a mine have a number in it that indicates the total number of mines in the neighboring cells. Starting off with some arrangement of mines we want to create a Minesweeper game setup.
```java
int[][] minesweeper(boolean[][] matrix) {
    int result[][] = new int[matrix.length][matrix[0].length];
    for(int i=0; i<matrix.length; i++){
        for(int j=0; j<matrix[0].length; j++){
            if(matrix[i][j]==true){
                for(int k=-1; k<2; k++){
                    for(int l = -1; l<2; l++){
                        if(i+k>=0 && j+l>=0 && i+k<matrix.length && j+l<matrix[0].length){
                            result[i+k][j+l]++;
                        }
                    }
                }
                result[i][j]--;
            }
        }
    }
    return result;
}
```