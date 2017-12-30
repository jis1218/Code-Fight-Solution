Sudoku is a number-placement puzzle. The objective is to fill a 9 × 9 grid with digits so that each column, each row, and each of the nine 3 × 3 sub-grids that compose the grid contains all of the digits from 1 to 9.
This algorithm should check if the given grid of numbers represents a correct solution to Sudoku.
Example
For the first example below, the output should be true. For the other grid, the output should be false: each of the nine 3 × 3 sub-grids should contain all of the digits from 1 to 9.

```java
boolean sudoku(int[][] grid) {

    TreeSet<Integer> set = new TreeSet<>();

    for(int l=0; l<3; l++){
        for(int m=0; m<3; m++){
            int sum = 0;            
            for(int i=3*l; i<3*l+3; i++){
                for(int j=3*m; j<3*m+3; j++){
                    set.add(grid[i][j]);
                    sum += grid[i][j];
                }
            }            
            if(set.size()!=9 || sum!=45){
                return false;
            }
        }
    }

    for(int i=0; i<9; i++){
        int sum2 = 0;
        int sum3 = 0;
        for(int j=0; j<9; j++){
            sum2+=grid[i][j];
            sum3+=grid[j][i];
        }

        if(sum2!=45 || sum3!=45){
            return false;
        }
    }

    return true;
}
```
