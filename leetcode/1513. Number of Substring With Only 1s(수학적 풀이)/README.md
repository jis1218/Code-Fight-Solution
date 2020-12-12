```java
class Solution {
    int MOD = 1000000007;
    public int numSub(String s) {
        int answer = 0;
        ArrayList<Integer> list = new ArrayList<>();
        int count = 0;
        s += "0";
        for(int i=0; i<s.length(); i++){
            if(s.charAt(i)=='1'){
                count++;
            }else{
                if(count!=0){
                    list.add(count);
                }
                count=0;
            }
        }
        for(int i : list){
            //System.out.println(i);
            //System.out.println(get(i));
            answer += get(i)%MOD;
        }
        return answer;
        
    }
    
    public int get(int n){
        return (int)((long)n*((long)n+1)/2%MOD);
    }
}
```