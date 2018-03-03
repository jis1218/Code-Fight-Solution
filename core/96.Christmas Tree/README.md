```java
String[] christmasTree(int levelNum, int levelHeight) {
    String[] result = new String[3+levelNum*levelHeight+levelNum];
    Arrays.fill(result, "");
    
    for(int i=0; i<levelNum; i++){        
        for(int k=3+i*levelHeight; k<=3+(i+1)*levelHeight-1; k++){
            for(int j=0; j<2*k-1; j++){  
                result[k] += "*";            
            }  
            System.out.println(result[k]);
        }
        
    }
    return result;
}
```