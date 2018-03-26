Sudoku is a number-placement puzzle. The objective is to fill a 9 × 9 grid with digits so that each column, each row, and each of the nine 3 × 3 sub-grids that compose the grid contains all of the digits from 1 to 9.
This algorithm should check if the given grid of numbers represents a correct solution to Sudoku.
Example
For the first example below, the output should be true. For the other grid, the output should be false: each of the nine 3 × 3 sub-grids should contain all of the digits from 1 to 9.
```java
boolean sudoku(int[][] grid) {
    for(int i=0; i<9; i++){
        int[] ref1 = new int[9];
        int[] ref2 = new int[9];
        for(int j=0; j<9; j++){            
            ref1[grid[i][j]-1]++;
            ref2[grid[j][i]-1]++;
            if(ref1[grid[i][j]-1]>1 || ref2[grid[j][i]-1]>1){
                return false;
            }
        }
    }    
    for(int m=0; m<3; m++){
        for(int n=0; n<3; n++){
            int[] ref3 = new int[9];
            for(int i=3*m; i<3*m+3; i++){       
                for(int j=3*n; j<3*n+3; j++){
                    ref3[grid[i][j]-1]++;
                    if(ref3[grid[i][j]-1]>1){
                        return false;
                    }
                }
            }            
        }
    }       
    return true;
}
```