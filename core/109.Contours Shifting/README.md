int[][] contoursShifting(int[][] matrix) {
    int rowLen = matrix.length;
    int colLen = matrix[0].length;
    int result[][] = new int[rowLen][colLen];
    int firstRow = 0;
    int firstColumn = 0;

    int count = 0;
    
    while(true){
        rotate(result, matrix, rowLen, colLen, firstRow, firstColumn, count);
        System.out.println(count);
        if(rowLen<3 || colLen<3){
            break;
        }
        rowLen -= 2;
        colLen -= 2;
        count++;
        firstRow++;
        firstColumn++;
    }
    
    
    return result;
    
}

void rotate(int first[][], int second[][], int rowLen, int colLen, int firstRow, int firstColumn, int count){

    if(count%2==0){
        if(rowLen==1){
            int temp = second[firstRow][firstColumn+colLen-1];

            for(int i=firstColumn; i<firstColumn+colLen-1; i++){
            first[firstRow][i+1] = second[firstRow][i];
            }
            first[firstRow][firstColumn] = temp;
        }else if(colLen==1){
            int temp = second[firstRow+rowLen-1][firstColumn];

            for(int i=firstRow; i<firstRow+rowLen-1; i++){
                first[i+1][firstColumn+colLen-1] = second[i][firstColumn+colLen-1];
            }
            first[firstRow][firstColumn] = temp;        
        }else{
            for(int i=firstColumn; i<firstColumn+colLen-1; i++){
                first[firstRow][i+1] = second[firstRow][i];
            }
            for(int i=firstRow; i<firstRow+rowLen-1; i++){
                first[i+1][firstColumn+colLen-1] = second[i][firstColumn+colLen-1];
            }
            for(int i=firstColumn; i<firstColumn+colLen-1; i++){
                first[firstRow+rowLen-1][i] = second[firstRow+rowLen-1][i+1];
            }
            for(int i=firstRow; i<firstRow+rowLen-1; i++){
                first[i][firstColumn] = second[i+1][firstColumn];
            }            
        }
        
    }else{
        if(rowLen==1){
            int temp = second[firstRow][firstColumn];
            for(int i=firstColumn; i<firstColumn+colLen-1; i++){
            first[firstRow][i] = second[firstRow][i+1];
            }
            first[firstRow][firstColumn+colLen-1] = temp;
        }else if(colLen==1){
            int temp = second[firstRow][firstColumn];
            for(int i=firstRow; i<firstRow+rowLen-1; i++){
                first[i][firstColumn+colLen-1] = second[i+1][firstColumn+colLen-1];
            }
            first[firstRow+rowLen-1][firstColumn] = temp;
        }else{
            for(int i=firstColumn; i<firstColumn+colLen-1; i++){
                first[firstRow+rowLen-1][i+1] = second[firstRow+rowLen-1][i];
            }
            for(int i=firstRow; i<firstRow+rowLen-1; i++){
                first[i+1][firstColumn] = second[i][firstColumn];
            }
            for(int i=firstColumn; i<firstColumn+colLen-1; i++){
                first[firstRow][i] = second[firstRow][i+1];
            }
            for(int i=firstRow; i<firstRow+rowLen-1; i++){
                first[i][firstColumn+colLen-1] = second[i+1][firstColumn+colLen-1];
            }
        }
        
    }
    
}