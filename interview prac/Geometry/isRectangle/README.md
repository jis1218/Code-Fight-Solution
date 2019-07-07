You have four points in an array points = [[x1, y1], [x2, y2], [x3, y3], [x4, y4]]. You make a (possibly self-intersecting) 4-sided polygon by joining the adjacent points in the list and joining points[3] back to points[0]. Write a function that returns true if the shape formed by points is a rectangle, and false otherwise.
##### 쉬운 문제였음
```java
boolean isRectangle(int[][] points) {
    return points[0][0]+points[2][0]==points[1][0]+points[3][0]
        && points[0][1]+points[2][1]==points[1][1]+points[3][1]
        && Math.pow(points[0][0]-points[2][0],2)+Math.pow(points[0][1]-points[2][1],2)
        == Math.pow(points[1][0]-points[3][0],2)+Math.pow(points[1][1]-points[3][1],2);

}
```
