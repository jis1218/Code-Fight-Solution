Imagine a standard chess board with only two white and two black knights placed in their standard starting positions: the white knights on b1 and g1; the black knights on b8 and g8.
There are two players: one plays for white, the other for black. During each move, the player picks one of his knights and moves it to an unoccupied square according to standard chess rules. Thus, a knight on d5 can move to any of the following squares: b6, c7, e7, f6, f4, e3, c3, and b4, as long as it is not occupied by either a friendly or an enemy knight.
The players take turns in making moves, starting with the white player. Given the configuration p of the knights after an unspecified number of moves, determine whose turn it is.
```java
boolean whoseTurn(String p) {
    String knights[] = p.split(";");
    int white = knights[0].charAt(0) + knights[0].charAt(1) + knights[1].charAt(0) + knights[1].charAt(1);
    int black = knights[2].charAt(0) + knights[2].charAt(1) + knights[3].charAt(0) + knights[3].charAt(1);
    
    return (white+black)%2==0;
}
```
##### 내 풀이도 꽤 괜찮았다고 생각했는데 이런 풀이가 가능하군...
##### 예를들어 p의 hashcode를 이용하였다. p.hashcode()가 홀수이냐 짝수이냐에 따라 답이 나오기 때문에 이런 풀이가 가능, p가 string 값이기 때문에 가능한 풀이이다.
```java
boolean whoseTurn(String p) {
	return (~p.hashCode() & 1) == 0;
}
```