```java
boolean[][] livingOnTheRoads(boolean[][] roadRegister) {
    ArrayList<int[]> list = new ArrayList<>();
    
    for(int i=0; i<roadRegister.length; i++){
        for(int j=i+1; j<roadRegister[0].length; j++){
            if(roadRegister[i][j]){
                int[] temp = new int[2];
                temp[0] = i;
                temp[1] = j;
                list.add(temp);
            }
        }
    }
    
    boolean[][] result = new boolean[list.size()][list.size()];
    
    for(int i=0; i<list.size(); i++){
        for(int j=0; j<i; j++){
            if(isSame(list.get(i), list.get(j))){
                result[i][j] = true;
                result[j][i] = true;
            }
        }
    }
    
    return result;
}

boolean isSame(int[] a, int[] b){
    return a[0]==b[0] || a[1]==b[0] || a[0]==b[1] || a[1]==b[1];
}
```