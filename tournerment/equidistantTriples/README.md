Consider several points lying on a straight line. Call an unordered triple of points an equidistant triple if one of them is the mid-point of the segment formed by the other two.
Given the coordinates of the points, find the number of equidistant triples formed by them.
Example
For coordinates = [1, 2, 4, 6, 7, 8], the output should be
equidistantTriples(coordinates) = 4.
The equidistant triples are: (1, 4, 7), (2, 4, 6), (4, 6, 8), (6, 7, 8).
```java
int equidistantTriples(int[] coordinates) {
    int result = 0;
    for(int i=0; i<coordinates.length-2; i++){
        for(int j=i+2; j<coordinates.length; j++){
            for(int m=i+1; m<j; m++){
                if(coordinates[i]+coordinates[j]==2*coordinates[m]){
                    result++;
                }
            }
        }
    }

    return result;

}
```
