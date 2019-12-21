```java
import java.util.*;
class Solution {
    HashMap<Integer, Integer> map = new HashMap<>();
    public int solution(int[][] baseball) {
        List<Integer> list = new ArrayList<>();
        for(int i=111; i<=999; i++){
            if(!sameNum(i)){
                list.add(i);
                //System.out.println(i);
            } 
        }
        
        for(int i=0; i<baseball.length; i++){            
            for(int k=list.size()-1; k>=0; k--){
                if(!ref(baseball[i][1], baseball[i][2], list.get(k), baseball[i][0])){
                    list.remove(k);
                }
            }            
        }
        
        return list.size();
    }    
    public boolean sameNum(int num){
        int a = num/100;
        int b = (num%100)/10;
        int c = (num%100)%10;
        if(a==b || b==c || a==c || a==0 || b==0 || c==0) return true;
        return false;
    }
    
    public boolean ref(int strike, int ball, int num1, int num2){
        int str = 0;
        int ba = 0;
        String s1 = String.valueOf(num1);
        String s2 = String.valueOf(num2);
        for(int i=0; i<3; i++){
            for(int j=0; j<3; j++){
                if(s1.charAt(i)==s2.charAt(j)){
                    if(i==j) str++;
                    else ba++;
                }
            }
        }
        return str==strike && ba==ball;
    }

}
```