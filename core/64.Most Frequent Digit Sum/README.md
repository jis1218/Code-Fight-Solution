Given a rectangular matrix containing only digits, calculate the number of different 2 × 2 squares in it.
Example
For
matrix = [[1, 2, 1],
          [2, 2, 2],
          [2, 2, 2],
          [1, 2, 3],
          [2, 2, 1]]
the output should be
differentSquares(matrix) = 6.

```java
int differentSquares(int[][] matrix) {
    ArrayList<int[][]> list = new ArrayList<>();
    int result = 0;
    
    for(int i=0; i<matrix.length-1; i++){
        for(int j=0; j<matrix[0].length-1; j++){
            
            int[][] arr = new int[2][2];
            
            for(int m=0; m<2; m++){
                for(int n=0; n<2; n++){
                    arr[m][n] = matrix[m+i][n+j];                    
                }
            }
            
            
            for(int k=0; k<list.size(); k++){
                boolean flag = true;
                for(int l=0; l<2; l++){
                    if(!Arrays.equals(arr[l], list.get(k)[l])){
                        flag = false;
                        break;
                    }
                }
                if(flag){
                    result++;
                    break;
                }
            }
            list.add(arr);
        }
    }
    
    return list.size()-result;

}
```

##### 처음에 Set을 이용하여 풀려고 하였으나 set이 2차원 배열을 걸러내지 못함
##### 좋은 풀이 중에 아래와 같은 풀이가 있었음
```java
int differentSquares(int[][] a) {
    Set<Integer> set = new TreeSet();
    for(int i = 0; i+1 < a.length ; i++){
        for(int j = 0 ; j+1 < a[0].length; j++){
            int num = a[i][j] * 1000 + a[i][j+1] * 100 + a[i+1][j] * 10 + a[i+1][j+1];
            set.add(num);
        }
    }
    
    return set.size();
}
```