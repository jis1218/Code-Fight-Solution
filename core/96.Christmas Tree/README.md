It's Christmas time! To share his Christmas spirit with all his friends, the young Christmas Elf decided to send each of them a Christmas e-mail with a nice Christmas tree. Unfortunately, Internet traffic is very expensive in the North Pole, so instead of sending an actual image he got creative and drew the tree using nothing but asterisks ('*' symbols). He has given you the specs (see below) and your task is to write a program that will generate trees following the spec and some initial parameters.
```java
String[] christmasTree(int levelNum, int levelHeight) {
    String[] result = new String[3+levelNum*levelHeight+levelNum];
    Arrays.fill(result, "");
    
    String a = "";
    for(int i=0; i<levelHeight+levelNum-1; i++){
        a += " ";
    }
    // 1, 2, 3번째 층
    result[2] = a + "***";
    result[0] = a + " *";
    result[1] = a + " *";
    
    int finAstro = 0;    
    
    for(int i=0; i<levelNum; i++){        
        for(int k=3+i*levelHeight; k<=3+(i+1)*levelHeight-1; k++){
            for(int m=0; m<3+(i+1)*levelHeight+levelNum-i-2-k; m++){
                result[k] += " ";
            }
            for(int j=0; j<2*(k-i*(levelHeight-1))-1; j++){  
                result[k] += "*";   
                finAstro = j;
            }  
            System.out.println(result[k]);
        }        
    }    
    
    int modified = levelHeight%2==0?levelHeight+1:levelHeight;
    
    // root 구하는 방법 - (마지막 별의 개수/2 - levelHeight/2)
    for(int k=result.length-1; k>result.length-1-levelNum; k--){
        for(int i=0; i<(finAstro/2-levelHeight/2); i++){
            result[k]+= " ";
        }        
        for(int i=0; i<modified; i++){
            result[k]+= "*";
        }
    }    
    return result;
}
```