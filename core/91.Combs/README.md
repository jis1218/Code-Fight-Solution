Miss X has only two combs in her possession, both of which are old and miss a tooth or two. She also has many purses of different length, in which she carries the combs. The only way they fit is horizontally and without overlapping. Given teeth' positions on both combs, find the minimum length of the purse she needs to take them with her.
It is guaranteed that there is at least one tooth at each end of the comb.
It is also guaranteed that the total length of two strings is smaller than 32.
Note, that the combs can not be rotated/reversed.
Example
For comb1 = "*..*" and comb2 = "*.*", the output should be
combs(comb1, comb2) = 5.
Although it is possible to place the combs like on the first picture, the best way to do this is either picture 2 or picture 3.
##### 나의 풀이 - comb1에 comb1+com2까지 되도록 "."를 넣었음, 코드가 더 복잡해짐
```java
int combs(String comb1, String comb2) {
    return Math.min(find(comb1, comb2), find(comb2, comb1));
}

int find(String comb1, String comb2){
    int min = comb1.length() + comb2.length();
    for(int i=0; i<comb2.length(); i++){
        comb1 += ".";
    }
    for(int i=0; i<comb1.length()-comb2.length(); i++){
        int temp = i;
        boolean flag = true;
        for(int j=0; j<comb2.length(); j++){            
            if(comb1.charAt(temp)=='*' && comb2.charAt(j)=='*'){
                flag = false;
                break;
            }
            temp++;
        }
        if(flag){
            System.out.println(i);
            if(comb1.length()-comb2.length()-i>comb2.length()){
                min = comb1.length()-comb2.length();
            }else{
                min = i + comb2.length();  
            }
            break;
        }
    }    
    return min;
}
```

##### 완벽한 풀이는 아니나 접근 방법이 나와 비슷하지만 더 좋음
```java
int combs(String comb1, String comb2) {
    int best = comb1.length() + comb2.length();
    for (int i = 0; i < comb1.length(); i++) {
        boolean can = true;
        for (int j = 0; j < comb2.length() && i+j < comb1.length(); j++) { //특히 이 부분이 정말 좋다.
            if (comb1.charAt(i+j) == '*' && comb2.charAt(j) == '*') {
                can = false;
                j = comb2.length();
            }
        }
        if (can && (i + comb2.length()) < best)
            best = i + comb2.length();
    }
    if (best < comb1.length())
        return comb1.length();
    return best;
}
```