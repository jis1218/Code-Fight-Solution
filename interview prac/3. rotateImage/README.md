Note: Try to solve this task in-place (with O(1) additional memory), since this is what you'll be asked to do during an interview.
You are given an n x n 2D matrix that represents an image. Rotate the image by 90 degrees (clockwise).
Example
For
a = [[1, 2, 3],
     [4, 5, 6],
     [7, 8, 9]]
the output should be
rotateImage(a) =
    [[7, 4, 1],
     [8, 5, 2],
     [9, 6, 3]]
##### in-place로 풀어야 하는데 아래 풀이가 in-place가 맞는지 모르겠다. 왜냐면 구글에는 in-place를 따로 변수를 설정하지 않고 그 안에서 푸는 것으로 나와 있기 때문이다. 일단 내 풀이는 이렇고
```java
int[][] rotateImage(int[][] a) {
    
    int b[][] = new int[a.length][a.length];
    
    for(int i=0; i<a.length; i++){
        for(int j=0; j<a.length; j++){
            b[j][a.length-1-i] = a[i][j];
        }
    }
    
    return b;
}
```

##### 고수의 풀이는 다음과 같다. 역시나 따로 변수를 설정하지 않았다.
```java
int[][] rotateImage(int[][] a) {
    int n = a.length;
    for(int i = 0; i < n / 2; i++){
        for(int j = i; j < n-i-1; j++){
            int temp = a[i][j];
            a[i][j] = a[n-j-1][i];
            a[n-j-1][i] = a[n-1-i][n-1-j];
            a[n-1-i][n-1-j] = a[j][n-1-i];
            a[j][n-1-i] = temp;
        }
    }
    return a;
}
```