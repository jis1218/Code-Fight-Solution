Pawn race is a game for two people, played on an ordinary 8 × 8 chessboard. The first player has a white pawn, the second one - a black pawn. Initially the pawns are placed somewhere on the board so that the 1st and the 8th rows are not occupied. Players take turns to make a move.
White pawn moves upwards, black one moves downwards. The following moves are allowed:
one-cell move on the same vertical in the allowed direction;
two-cell move on the same vertical in the allowed direction, if the pawn is standing on the 2nd (for the white pawn) or the 7th (for the black pawn) row. Note that even with the two-cell move a pawn can't jump over the opponent's pawn;
capture move one cell forward in the allowed direction and one cell to the left or to the right.

The purpose of the game is to reach the the 1st row (for the black pawn) or the 8th row (for the white one), or to capture the opponent's pawn.
Given the initial positions and whose turn it is, determine who will win or declare it a draw (i.e. it is impossible for any player to win). Assume that the players play optimally.
Example
For white = "e2", black = "e7" and toMove = 'w', the output should be
pawnRace(white, black, toMove) = "draw";
For white = "e3", black = "d7" and toMove = 'b', the output should be
pawnRace(white, black, toMove) = "black";
For white = "a7", black = "h2" and toMove = 'w', the output should be
pawnRace(white, black, toMove) = "white".

##### 경우의 수를 많이 생각해야 한다. 특히 흑과 백이 같은 파일에 있으면서 백과 흑이 만나지 않는 경우가 있을 수 있다.
```java
String pawnRace(String white, String black, char toMove) {
    
    int white1 = white.charAt(0);
    int white2 = white.charAt(1);
    int black1 = black.charAt(0);
    int black2 = black.charAt(1);
    
    if(white1==black1){
        if(white2>=black2){
            if('8'-white2>black2-'1'){
            return "black";
        }else if('8'-white2<black2-'1'){
            return "white";
        }else if('8'-white2==black2-'1'){
            if(toMove=='w') return "white";
            else return "black";
        }
            
        }else return "draw";
    }else if(white2>=black2){
        if('8'-white2>black2-'1') return "black";
        else if('8'-white2<black2-'1') return "white";
        else{
            if(toMove=='w') return "white";
            else return "black";
        }
    }else if(Math.abs(white1-black1)==1){        
        if((white2=='2' && black2=='7') || (white2=='2' && black2=='4') || (white2=='5' && black2=='7')){
            if(toMove=='w') return "black";
            else return "white";
        }else if((white2=='2' && (black2=='5'|| black2=='3')) || ((white2=='4'||white2=='6') && black2=='7')){
            if(toMove=='w') return "white";
            else return "black";
        }else if(white2=='2' && black2=='6'){
            return "white";
        }else if(black2=='7' && white2=='3'){
            return "black";
        }else if((black2-white2)%2==0){
            if(toMove=='w') return "black";
            else return "white";
        }else if((black2-white2)%2==1){
            if(toMove=='w') return "white";
            else return "black";
        }
    }else{
        if('8'-white2>black2-'1'){
            if(white2=='2' && black2=='6' && toMove=='w') return "white";
            return "black";
        }else if('8'-white2<black2-'1'){
            if(white2=='3' && black2=='7' && toMove=='b') return "black";
            return "white";
        }else if('8'-white2==black2-'1'){
            if(toMove=='w') return "white";
            else return "black";
        }
    }
    
    return "None"; 
}
```

##### 다른 사람들도 나와 비슷하게 푼것 같다.