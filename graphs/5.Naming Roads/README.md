Unfortunately the king didn't have enough time to come up with actual names, so all the roads were to be names with numbers from 0 to roads.length - 1. As a born strategist, Byteasar wanted to make sure that the maps of his kingdom were confusing to enemies, which is why the road names were to be chosen so that no two roads with the neighboring names (i.e. names i and i + 1 for some i) would have a common end at one of the cities.
The archicartographer came up with the names for the roads, but he was not sure if the constraint the king imposed was met. He asked the Greater Power to help him check it. As a Greater Power from the future, you are the one who can help with that. Given the names for the roads the archicartographer came up with, check that no two roads with the neighboring names have a common end.
Example
For
roads = [[0, 1, 0],
         [4, 1, 2],
         [4, 3, 4],
         [2, 3, 1],
         [2, 0, 3]]
the output should be
namingRoads(roads) = true.
Here's what the given road system looks like:

For
roads = [[2, 3, 1],
         [3, 0, 0],
         [2, 0, 2]]
the output should be
namingRoads(roads) = false.
```java
boolean namingRoads(int[][] roads) {
    Arrays.sort(roads,(a, b)->((Comparable)a[2]).compareTo(b[2]));
    for(int i=0; i<roads.length-1; i++){
        if(roads[i][0]==roads[i+1][1] || roads[i][0]==roads[i+1][0] || roads[i][1]==roads[i+1][0] || roads[i][1]==roads[i+1][1]){
            return false;
        }
    }    
    return true;
}
```

##### 위의 풀이는 다음과 같다는 것을 잘 알아두자!
```java
boolean namingRoads(int[][] roads)
{
    Arrays.sort(roads, new Comparator<int[]>() {
        @Override
        public int compare(int[] o1, int[] o2)
        {
            return o1[2] - o2[2];
        }
    });
    
    for (int i = 1; i < roads.length; i++)
    {
        if (roads[i][0] == roads[i-1][1] || roads[i-1][0] == roads[i][1])
        {
            return false;
        }
    }
    
    return true;
}
```