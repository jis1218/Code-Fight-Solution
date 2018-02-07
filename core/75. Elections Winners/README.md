Elections are in progress!
Given an array of the numbers of votes given to each of the candidates so far, and an integer k equal to the number of voters who haven't cast their vote yet, find the number of candidates who still have a chance to win the election.
The winner of the election must secure strictly more votes than any other candidate. If two or more candidates receive the same (maximum) number of votes, assume there is no winner at all.

```java
int electionsWinners(int[] votes, int k) {
    int max = 0;
    int result = 0;
    int index = 0;
    for(int i : votes){
        if(i>max) max=i;
    }    
    for(int i : votes){
        if(i+k>max) result++;
        else if(i+k==max){
            if(k==0){
                index++;
            }
        }
    }    
    if(index==1){
        return 1;
    }    
    return result;
}
```