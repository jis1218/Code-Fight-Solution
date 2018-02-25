Yesterday you found some shoes in the back of your closet. Each shoe is described by two values:
type indicates if it's a left or a right shoe;
size is the size of the shoe.
Your task is to check whether it is possible to pair the shoes you found in such a way that each pair consists of a right and a left shoe of an equal size.
##### 첫번째 풀이
```java
boolean pairOfShoes(int[][] shoes) {
    int sum1 = 0;
    int sum2 = 0;
    int count1 = 0;
    int count2 = 0;
    
    for(int i=0; i<shoes.length; i++){
        if(shoes[i][0]==0){
            sum1 += shoes[i][1];
            count1++;
        }else{
            sum2 += shoes[i][1];
            count2++;
        }
    }
    
    if(count1!=count2 || sum1!=sum2) return false;
    
    return true;
}
```
##### 잘 된 풀이
```java
boolean pairOfShoes(int[][] shoes) {
    int[] types = new int[101];
    for (int[] i : shoes) {
        if (i[0] == 0)
            types[i[1]]--; //오직 하나의 array로 균형이 맞는지 아닌지 알 수 있음
        else
            types[i[1]]++;
    }
    for (int i : types)
        if (i != 0)
            return false;
    return true;
}
```