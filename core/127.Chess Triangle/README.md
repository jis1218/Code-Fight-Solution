Consider a bishop, a knight and a rook on an n × m chessboard. They are said to form a triangle if each piece attacks exactly one other piece and is attacked by exactly one piece. Calculate the number of ways to choose positions of the pieces to form a triangle.
Note that the bishop attacks pieces sharing the common diagonal with it; the rook attacks in horizontal and vertical directions; and, finally, the knight attacks squares which are two squares horizontally and one square vertically, or two squares vertically and one square horizontally away from its position.

##### 체스판이 주어졌을 때 각 크기의 가지수를 찾는 것이 중요
```java
int chessTriangle(int n, int m) {
    
    int a = (n+1-3)*(m+1-2); 
    int b = (n+1-2)*(m+1-3);
    int c = (n+1-3)*(m+1-3);
    int d = (n+1-4)*(m+1-2);
    int e = (n+1-2)*(m+1-4);
    int f = (n+1-3)*(m+1-4);
    int g = (n+1-4)*(m+1-3);
    
    if(a<1) a = 0;
    if(b<1) b = 0;
    if(c<1) c = 0;
    if(d<1) d = 0;
    if(e<1) e = 0;
    if(f<1) f = 0;
    if(g<1) g = 0;
    
    return 8*(a+b) + 16*c + 8*(d+e) + 8*(f+g);
}
```