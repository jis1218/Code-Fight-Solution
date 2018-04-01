int[][] contoursShifting(int[][] matrix) {
    
    int temp = matrix[0][0];
    for(int i=0; i<matrix.length-1; i++){
        matrix[i][0] = matrix[i+1][0];
    }
    
    for(int i=0; i<matrix[0].length-1; i++){
        matrix[matrix.length-1][i] =  matrix[matrix.length-1][i+1];
    }
    for(int i=matrix.length-1; i>0; i--){
        matrix[i][matrix[0].length-1] = matrix[i-1][matrix[0].length-1];        
    }
    if(matrix[0].length!=1){
       for(int i=matrix[0].length-1; i>1; i--){
            matrix[0][i] = matrix[0][i-1];
        } 
    }    
    
    matrix[0][1] = temp;
    
    return matrix;
}