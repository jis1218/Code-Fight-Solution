Given a position of a knight on the standard chessboard, find the number of different moves the knight can perform.
The knight can move to a square that is two squares horizontally and one square vertically, or two squares vertically and one square horizontally away from it. The complete move therefore looks like the letter L. Check out the image below to see all valid moves for a knight piece that is placed on one of the central squares.
```java
int chessKnightMoves(String cell) {
    int first = cell.charAt(0);
    int second = cell.charAt(1);
    int result = 8;
    
    if(first-2-'a'<0 || second-1-'1'<0) result--;
    if(first-2-'a'<0 || '8'-second-1<0) result--;
    if(first-1-'a'<0 || second-2-'1'<0) result--;
    if(first-1-'a'<0 || '8'-second-2<0) result--;
    if('h'-first-2<0 || second-1-'1'<0) result--;
    if('h'-first-2<0 || '8'-second-1<0) result--;
    if('h'-first-1<0 || second-2-'1'<0) result--;
    if('h'-first-1<0 || '8'-second-2<0) result--;
    
    
    return result;
}
```

##### 다른 풀이
```java
int chessKnightMoves(String cell) {
    int x = cell.charAt(0) - 'a';
    int y = cell.charAt(1) - '1';
    if (x > 3)
        x = 7-x;
    if (y > 3)
        y = 7-y;
    if (x < y) {
        int temp = x;
        x = y;
        y = temp;
    }
    if (y > 1)
        return 8;
    if (x > 1)
        return 4 + 2*y;
    if (x == 1)
        return 3 + y;
    return 2;
}
```