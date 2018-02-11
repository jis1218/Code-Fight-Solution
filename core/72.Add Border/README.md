Given a rectangular matrix of characters, add a border of asterisks(*) to it.
```java
String[] addBorder(String[] picture) {
    
    String res[] = new String[picture.length+2];
    
    String star = "";
    for(int i=0; i<picture[0].length()+2; i++){
        star += "*";
    }
    
    for(int i=1; i<res.length-1; i++){
        res[i] = "*" + picture[i-1] + "*";
    }
    
    res[0] = star;
    res[res.length-1] = star;
    
    return res;
}
```