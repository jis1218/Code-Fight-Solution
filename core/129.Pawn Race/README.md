```java
String pawnRace(String white, String black, char toMove) {
    
    int white1 = white.charAt(0);
    int white2 = white.charAt(1);
    int black1 = black.charAt(0);
    int black2 = black.charAt(1);
    
    if(white1==black1) return "draw";
    else if(white2>=black2){
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