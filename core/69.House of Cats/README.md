There are some people and cats in a house. You are given the number of legs they have all together. Your task is to return an array containing every possible number of people that could be in the house sorted in ascending order. It's guaranteed that each person has 2 legs and each cat has 4 legs.
```java
int[] houseOfCats(int legs) {
    int div = legs/4;
    int res[] = new int[div+1];
    
    for(int i=0; i<res.length; i++){
        
        res[i] = (legs-div*4)/2;
        div--;        
    }    
    return res;
}
```