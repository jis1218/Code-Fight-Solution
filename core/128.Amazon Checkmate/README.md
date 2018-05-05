An amazon (also known as a queen+knight compound) is an imaginary chess piece that can move like a queen or a knight (or, equivalently, like a rook, bishop, or knight). The diagram below shows all squares which the amazon attacks from e4 (circles represent knight-like moves while crosses correspond to queen-like moves).

Recently you've come across a diagram with only three pieces left on the board: a white amazon, white king and black king. It's black's move. You don't have time to determine whether the game is over or not, but you'd like to figure it out in your head. Unfortunately, the diagram is smudged and you can't see the position of the black's king, so it looks like you'll have to check them all.
Given the positions of white pieces on a standard chessboard, determine the number of possible black king's positions such that:
it's checkmate (i.e. black's king is under amazon's attack and it cannot make a valid move);
it's check (i.e. black's king is under amazon's attack but it can reach a safe square in one move);
it's stalemate (i.e. black's king is on a safe square but it cannot make a valid move);
black's king is on a safe square and it can make a valid move.
Note that two kings cannot be placed on two adjacent squares (including two diagonally adjacent ones).

##### 대부분의 풀이가 체스판을 그려서 풀었다.
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
            if((que1==i && que2==j) && (king1-1<=i && i<=king1+1 && king2-1<=j && king2+1>=j)){ //킹이 퀸을 보호하고 있을 경우
                chessBoard[i][j] = 9;
            }else if((que1==i && que2==j)){ //퀸의 위치
                chessBoard[i][j] = 7;
            }else if((king1-1<=i && i<=king1+1 && king2-1<=j && king2+1>=j)){ //킹의 범위
                chessBoard[i][j] = 8;
            }else if((Math.abs(que1-i)==Math.abs(que2-j)) && (Math.abs(king1-i)==Math.abs(king2-j)) && (king1-que1)*(i-king1)>0 && (king2-que2)*(j-king2)>0){ //킹과 퀸이 대각선에 있을 경우
                chessBoard[i][j] = 2;
            }else if((king1==que1 && i==que1 && (king2-j)*(que2-king2)>0) || (king2==que2 && j==que2 && (king1-i)*(que1-king1)>0) ){ //킹과 퀸이 같은 행 또는 열에 있을 경우
                chessBoard[i][j] = 2;
                
            }else if((Math.abs(que1-i)==Math.abs(que2-j)) || que1==i || que2==j || (Math.abs(i-que1)==1 && Math.abs(j-que2)==2) ||
               (Math.abs(i-que1)==2 && Math.abs(j-que2)==1)){                
                chessBoard[i][j] = 1;         //체크인 경우        
            }else{
                chessBoard[i][j] = 2; // 안전한 경우
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

##### 전 풀이는 다음과 같았다. 킹과 퀸이 대각선, 같은 행 또는 열에 있을 경우의 조건이 잘못 되었다.
```java
int[] amazonCheckmate(String king, String amazon) {

            }else if((Math.abs(que1-i)==Math.abs(que2-j)) && (Math.abs(king1-i)==Math.abs(king2-j)) && (Math.abs(que1-i)>Math.abs(king1-i))){
                chessBoard[i][j] = 2; //킹과 퀸이 대각선에 있을 경우
            }else if((que1 == king1 && i==que1 && Math.abs(que2-j)>Math.abs(king2-j)) || (que2==king2 && j==que2 && Math.abs(que1-i)>Math.abs(king1-i))){
                chessBoard[i][j] = 2; //킹과 퀸이 같은 행 또는 열에 있을 경우
```
