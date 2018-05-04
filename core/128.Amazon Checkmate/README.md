```java
int[] amazonCheckmate(String king, String amazon) {
    int result[] = new int[4];
    int checkmate = 0;
    int check = 0;
    int stalemate = 0;
    int safePosition = 0;
    
    int chessBoard[][] = new int[8][8];
    
    int king1 = king.charAt(0)-'a';
    int king2 = king.charAt(1)-'1';
    int que1 = amazon.charAt(0)-'a';
    int que2 = amazon.charAt(1)-'1';
    
    // 체크인 경우 : 1
    // 안전한 경우 : 2
    // 킹의 범위 : 8
    // 퀸의 자리 : 7
    // 보호받는 퀸 : 9
    
    for(int i=0; i<8; i++){
        for(int j=0; j<8; j++){
            if((que1==i && que2==j) && (king1-1<=i && i<=king1+1 && king2-1<=j && king2+1>=j)){
                chessBoard[i][j] = 9;
            }else if((que1==i && que2==j)){
                chessBoard[i][j] = 7;
            }else if((king1-1<=i && i<=king1+1 && king2-1<=j && king2+1>=j)){
                chessBoard[i][j] = 8;
            }else if((Math.abs(que1-i)==Math.abs(que2-j)) && (Math.abs(king1-i)==Math.abs(king2-j)) && (Math.abs(que1-i)>Math.abs(king1-i))){
                chessBoard[i][j] = 2;
            }else if((que1 == king1 && i==que1 && Math.abs(que2-j)>Math.abs(king2-j)) || (que2==king2 && j==que2 && Math.abs(que1-i)>Math.abs(king1-i))){
                chessBoard[i][j] = 2;
            }else if((Math.abs(que1-i)==Math.abs(que2-j)) || que1==i || que2==j || (Math.abs(i-que1)==1 && Math.abs(j-que2)==2) ||
               (Math.abs(i-que1)==2 && Math.abs(j-que2)==1)){                
                chessBoard[i][j] = 1;                
            }else{
                chessBoard[i][j] = 2;
            }  
        }
    }
    
    for(int i=0; i<8; i++){
        for(int j=0; j<8; j++){
            System.out.print(chessBoard[i][j] + ", ");
        }
        System.out.println("\n");
    }
    
    for(int i=0; i<8; i++){
        for(int j=0; j<8; j++){
            int index = 0;            
            for(int k=i-1; k<=i+1; k++){                
                for(int m=j-1; m<=j+1; m++){
                    if(k>=0 && k<8 && m>=0 && m<8 && (k!=i || m!=j)){
                        
                        if(chessBoard[i][j]==1){
                            if(chessBoard[k][m]!=1 && chessBoard[k][m]!=8 && chessBoard[k][m]!=9){
                               
                                index = 2; //check
                                break;
                            }else{
                                index=1;
                            }  
                        }else if(chessBoard[i][j]==2){
                            if(chessBoard[k][m]!=1 && chessBoard[k][m]!=8 && chessBoard[k][m]!=9){
                                index = 3; //safeposition
                                break;
                            }else{
                                index = 4;
                            }
                        }                            
                    }
                }
                if(index==2 || index==3){
                    break;
                }
                
            }
            if(index==1){
                checkmate++;
            }else if(index==2){
                check++;
            }else if(index==3){
                safePosition++;
            }else if(index==4){
                stalemate++;
            }            
        }
    }    
    result[0] = checkmate;
    result[1] = check;
    result[2] = stalemate;
    result[3] = safePosition;
    
    return result;
}
```