You are given an array of desired filenames in the order of their creation. Since two files cannot have equal names, the one which comes later will have an addition to its name in a form of (k), where k is the smallest positive integer such that the obtained name is not used yet.
Return an array of names that will be given to the files.
Example
For names = ["doc", "doc", "image", "doc(1)", "doc"], the output should be
fileNaming(names) = ["doc", "doc(1)", "image", "doc(1)(1)", "doc(2)"].

##### 다른 풀이를 봐도 내 풀이가 가장 깔끔하고 군더더기가 없다.
```java
String[] fileNaming(String[] names) {
    for(int i=1; i<names.length; i++){
        String temp = "";
        int num = 1; 
        for(int j=0; j<i; j++){                       
            if((names[i].concat(temp)).equals(names[j])){
                temp = "(" + num + ")";
                num++;
                j=-1; //j를 -1로 해줘야 다음에 0이 된다.
            }                      
        }
        names[i] += temp;
    }    
    return names;
}
```