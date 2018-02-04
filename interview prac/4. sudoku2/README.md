Sudoku is a number-placement puzzle. The objective is to fill a 9 × 9 grid with numbers in such a way that each column, each row, and each of the nine 3 × 3 sub-grids that compose the grid all contain all of the numbers from 1 to 9 one time.
Implement an algorithm that will check whether the given grid of numbers represents a valid Sudoku puzzle according to the layout rules described above. Note that the puzzle represented by grid does not have to be solvable.
```java
boolean sudoku2(char[][] grid) {  
    for(int i=0; i<9; i++){
        int temp1[] = new int[10];
        int temp2[] = new int[10];
         int tem1=0;
         int tem2=0;
        for(int j=0; j<9; j++){
            if(grid[i][j]!='.' ) tem1 = ++temp1[grid[i][j]-48];            
            if(grid[j][i]!='.') tem2 = ++temp2[grid[j][i]-48];             
            if(tem1>1 || tem2>1) return false;            
        }        
    }  
    for(int i=0; i<3; i++){
        for(int j=0; j<3; j++){
            int temp1[] = new int[10];
            int tem = 0;            
            for(int k=3*i; k<3*i+3; k++){
                for(int l=3*j; l<3*j+3; l++){
                    if(grid[k][l]!='.') tem = ++temp1[grid[k][l]-48];
                    if(tem>1){
                        return false;
                    }
                }
            }            
        }
    }    
    return true;
}
```