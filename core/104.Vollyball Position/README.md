You are watching a volleyball tournament, but you missed the beginning of the very first game of your favorite team. Now you're curious about how the coach arranged the players on the field at the start of the game.
The team you favor plays in the following formation:
0 3 0
4 0 2
0 6 0
5 0 1
where positive numbers represent positions occupied by players. After the team gains the serve, its members rotate one position in a clockwise direction, so the player in position 2 moves to position 1, the player in position 3 moves to position 2, and so on, with the player in position 1 moving to position 6.
```java
String[][] volleyballPositions(String[][] formation, int k) {
    int[][] order = {{3, 2}, {1, 2}, {0, 1}, {1, 0}, {3, 0}, {2, 1}};
    String nameOrder[] = new String[6];
    
    for(int i=0; i<6; i++){
        nameOrder[i] = formation[order[i][0]][order[i][1]];
    }
    for(int i=0; i<k%6; i++){        
        int temp[] = Arrays.copyOf(order[0], order[0].length);
        
        for(int j=0; j<order.length-1; j++){
            order[j] = Arrays.copyOf(order[j+1], 2);
        }        
        order[5] = Arrays.copyOf(temp, 2);        
    }  
    
    String[][] result = new String[4][3];
    for(int i=0; i<4; i++){
        Arrays.fill(result[i], "empty");
    }

    for(int i=0; i<6; i++){
        result[order[i][0]][order[i][1]] = nameOrder[i];
    }
    
    return result;

}
```

##### 이렇게 풀어도 됨
String[][] volleyballPositions(String[][] formation, int k) {
    k = k%6;
    for (int i = 0; i < k; i++) {
        String temp = formation[3][2];
        formation[3][2] = formation[2][1];
        formation[2][1] = formation[3][0];
        formation[3][0] = formation[1][0];
        formation[1][0] = formation[0][1];
        formation[0][1] = formation[1][2];
        formation[1][2] = temp;
    }
    return formation;
}
```