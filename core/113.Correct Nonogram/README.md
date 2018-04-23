A nonogram is also known as Paint by Numbers and Japanese Crossword. The aim in this puzzle is to color the grid into black and white squares. At the top of each column, and at the side of each row, there are sets of one or more numbers which describe the runs of black squares in that row/column in exact order. For example, if you see 10 1 along some column/row, this indicates that there will be a run of exactly ten black squares, followed by one or more white squares, followed by a single black square. The cells along the edges of the grid can also be white.
You are given a square nonogram of size size. Its grid is given as a square matrix nonogramField of size (size + 1) / 2 + size, where the first (size + 1) / 2 cells of each row and and each column define the numbers for the corresponding row/column, and the rest size × size cells define the the grid itself.
Determine if the given nonogram has been solved correctly.
Note: here / means integer division.
Example
For size = 5 and
nonogramField = [["-", "-", "-", "-", "-", "-", "-", "-"],
                 ["-", "-", "-", "2", "2", "1", "-", "1"],
                 ["-", "-", "-", "2", "1", "1", "3", "3"],
                 ["-", "3", "1", "#", "#", "#", ".", "#"],
                 ["-", "-", "2", "#", "#", ".", ".", "."],
                 ["-", "-", "2", ".", ".", ".", "#", "#"],
                 ["-", "1", "2", "#", ".", ".", "#", "#"],
                 ["-", "-", "5", "#", "#", "#", "#", "#"]]
the output should be correctNonogram(size, nonogramField) = true;

##### 나의 풀이
```java
boolean correctNonogram(int size, String[][] nono) {
    int start = nono.length-size;
    
    for(int i=start; i<nono.length; i++){
        int index=0;
        for(int j=0; j<start; j++){            
            int cnt=0;
            if(!nono[i][j].equals("-")){ //숫자라면
                if(start+index>=nono.length){
                    return false;
                }
                if(nono[i][start+index].equals(".")){//에러가 여기서 발생한 것이었다. 숫자는 있는데 #이 없다면 .만 계속 찾는다 그러다가 index가 커져서 에러가 나는 것임
                    index++;
                    j = j-1;
                }else{
                    System.out.println(i + ", " + j + ", " + index);
                    for(int k=start+index; k<Integer.parseInt(nono[i][j])+start+index && k<nono.length; k++){
                        if(!nono[i][k].equals("#")){                            
                            return false;
                       }
                       cnt++;
                    }
                    index+=cnt;                
                    if(cnt!=Integer.parseInt(nono[i][j])){
                        System.out.println("cnt and parseInt not matched");
                        return false;
                    } 
                    
                    if(j==start-1){ //만약 마지막 숫자라면
                        for(int m=start+index; m<nono.length; m++){
                          if(nono[i][m].equals("#")){
                              System.out.println(m+"");
                             return false;
                            }
                        }
                    }else{//마지막 숫자가 아니라면 성공한 이후에 "."이 나와야 한다.
                        if(start+index>=nono.length){
                            return false;
                        }else if(nono[i][start+index].equals("#")){
                            System.out.println("after success . come");
                            return false;
                        }
                    }
                }                
            }
        }
    }
    
    for(int i=start; i<nono.length; i++){
        int index=0;
        for(int j=0; j<start; j++){            
            int cnt=0;
            if(!nono[j][i].equals("-")){ //숫자라면
                if(start+index>=nono.length){
                    return false;
                }
                if(nono[start+index][i].equals(".")){ //에러가 여기서 발생한 것이었다. 숫자는 있는데 #이 없다면 .만 계속 찾는다 그러다가 index가 커져서 에러가 나는 것임
                    index++;
                    j = j-1;
                }else{
                    System.out.println(i + ", " + j + ", " + index);
                    for(int k=start+index; k<Integer.parseInt(nono[j][i])+start+index && k<nono.length; k++){
                        if(!nono[k][i].equals("#")){
                            return false;
                        }
                        cnt++;
                    }
                    index+=cnt;
                
                    if(cnt!=Integer.parseInt(nono[j][i])){
                        System.out.println("cnt and parseInt not matched");
                        return false;
                    } 
                    
                    if(j==start-1){ //만약 마지막 숫자라면
                        for(int m=start+index; m<nono.length; m++){
                          if(nono[m][i].equals("#")){
                              System.out.println(m+"");
                             return false;
                            }
                        }
                    }else{//마지막 숫자가 아니라면 성공한 이후에 "."이 나와야 한다.
                        if(start+index>=nono.length){
                            return false;
                        }else if(nono[start+index][i].equals("#")){
                                System.out.println("after success . come");
                                return false;
                        }
                    }
                }                
            }
        }
    }
    
    return true;
}
```

##### 잘 안되었던 풀이, 결국 배열 outofindex error였다.
```java
boolean correctNonogram(int size, String[][] nono) {
    int start = nono.length-size;
    System.out.println(start+"");
    for(int i=start; i<nono.length; i++){
        int index=0;
        
        for(int j=0; j<start; j++){            
            if(!nono[i][j].equals("-")){
                int cnt=0;
                System.out.println(i+", " + j+", " + index);
                if(!nono[i][start+index].equals("#")){
                    index++;
                    j=j-1;
                                        
                }else{
                    for(int k=start+index; k<nono.length && k<start+index+Integer.parseInt(nono[i][j]); k++){
                        if(!nono[i][k].equals("#")){
                            System.out.println(i+", " + k);
                            return false;
                        }
                        cnt++;
                    }
                    index+= cnt+1;
                    if(cnt!=Integer.parseInt(nono[i][j])) return false;
                    if(j==start-1){
                        for(int m=start+index-1; m<nono.length; m++){
                            System.out.println(m+"");
                            if(nono[i][m].equals("#")){
                                return false;
                            }
                        }
                    }
                }                
            }                        
        }
    }
    
    for(int j=start; j<nono[0].length; j++){
        int index=0;        
        for(int i=0; i<start; i++){            
            if(!nono[i][j].equals("-")){
                int cnt=0;
                System.out.println(i+", " + j+", " + index);
                if(!nono[start+index][j].equals("#")){
                    index++;
                    i=i-1;                                        
                }else{
                    for(int k=start+index; k<nono.length && k<start+index+Integer.parseInt(nono[i][j]); k++){
                        if(!nono[k][j].equals("#")){
                            System.out.println(i+", " + k);
                            return false;
                        }
                        cnt++;
                    }
                    
                    index+= cnt+1;                    
                    if(cnt!=Integer.parseInt(nono[i][j])) return false;
                    if(i==start-1){
                        for(int m=start+index-1; m<nono.length; m++){
                            System.out.println(m+"");
                            if(nono[m][j].equals("#")){
                                return false;
                            }
                        }
                    }
                }                
            }  
            
        }  
    }
    
    return true;

}
```