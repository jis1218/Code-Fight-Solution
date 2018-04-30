In the Land Of Chess, bishops don't really like each other. In fact, when two bishops happen to stand on the same diagonal, they immediately rush towards the opposite ends of that same diagonal.
Given the initial positions (in chess notation) of two bishops, bishop1 and bishop2, calculate their future positions. Keep in mind that bishops won't move unless they see each other along the same diagonal.
Example
For bishop1 = "d7" and bishop2 = "f5", the output should be
bishopDiagonal(bishop1, bishop2) = ["c8", "h3"].
##### 별로 좋은 풀이는 아닌듯
```java
String[] bishopDiagonal(String bishop1, String bishop2) {
    String[] result = new String[2];
    int bi11 = bishop1.charAt(0)-'a';
    int bi12 = bishop1.charAt(1)-'1';
    int bi21 = bishop2.charAt(0)-'a';
    int bi22 = bishop2.charAt(1)-'1';
    
    if(Math.abs(bishop1.charAt(0)-bishop2.charAt(0))==Math.abs(bishop1.charAt(1)-bishop2.charAt(1))){
        System.out.println("hello");
        if(bi11-bi21>0 && bi12-bi22>0){
            System.out.println("should be1");
            while(bi11<7 && bi12<7){
                bi11++;
                bi12++;
            }
            while(bi21>0 && bi22>0){
                bi21--;
                bi22--;
            }
        }else if(bi11-bi21>0 && bi12-bi22<0){
            System.out.println("should be2");
            while(bi11<7 && bi12>0){
                bi11++;
                bi12--;
            }
            while(bi21>0 && bi22<7){
                bi21--;
                bi22++;
            }            
        }else if(bi11-bi21<0 && bi12-bi22>0){
            System.out.println("should be3");
            while(bi11>0 && bi12<7){
                bi11--;
                bi12++;
            }
            while(bi21<7 && bi22>0){
                bi21++;
                bi22--;
            }            
        }else if(bi11-bi21<0 && bi12-bi22<0){
            System.out.println("should be4");
            while(bi11>0 && bi12>0){
                bi11--;
                bi12--;
            }
            while(bi21<7 && bi22<7){
                bi21++;
                bi22++;
            }
        }
        
        result[0] = String.valueOf((char)(bi11+'a')) + String.valueOf((char)(bi12+'1'));
        result[1] = String.valueOf((char)(bi21+'a')) + String.valueOf((char)(bi22+'1'));
        Arrays.sort(result);
        return result;     
        
    }else{
        result[0] = bishop2;
        result[1] = bishop1;
        Arrays.sort(result);
        return result;
    }    
}
```

##### 이게 최고의 풀이인 듯... 상대적인 위치와 한 비숍의 위치만 잘 알고 있으면 나머지 비숍이 어디에 있던지 결국 대각선 끝으로 가는것은 마찬가지다. 이걸 이용해서 잘 풀었다.
```java
String[] bishopDiagonal(String b1, String b2) {
    char x = b1.charAt(0);
    char y = b1.charAt(1);
    if (x - y == b2.charAt(0) - b2.charAt(1)) {
        int d1 = Math.min(x - 'a', y - '1');
        int d2 = Math.min('h' - x, '8' - y);
        String r1 = "" + (char) (x - d1) + (char) (y - d1);
        String r2 = "" + (char) (x + d2) + (char) (y + d2);
        return new String[]{r1, r2};
    } else if (x + y == b2.charAt(0) + b2.charAt(1)) {
        int v1 = Math.min(x - 'a', '8' - y);
        int v2 = Math.min('h' - x, y - '1');
        String r1 = "" + (char) (x - v1) + (char) (y + v1);
        String r2 = "" + (char) (x + v2) + (char) (y - v2);
        return new String[]{r1, r2};
    }
    else if (b1.compareTo(b2) < 0) return new String[]{b1, b2};
    else return new String[]{b2, b1};
}
```