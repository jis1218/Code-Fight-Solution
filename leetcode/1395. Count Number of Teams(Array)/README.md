```java
class Solution {
    public int numTeams(int[] rating) {
        int sum = 0;
        for(int i=1; i<rating.length-1; i++){
            int lsmall=0, lbig=0, rsmall=0, rbig=0;
            for(int j=0; j<rating.length; j++){
                if(i>j){
                    if(rating[i]>rating[j]) lsmall++;
                    else lbig++;
                }else if(i<j){
                    if(rating[i]>rating[j]) rsmall++;
                    else rbig++;
                }
            }
            sum+=lbig*rsmall+rbig*lsmall;
        }
        return sum;
    }

}
```