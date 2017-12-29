Construct a square matrix with a size N × N containing integers from 1 to N * N in a spiral order, starting from top-left and in clockwise direction.
Example
For n = 3, the output should be
spiralNumbers(n) = [[1, 2, 3],
                    [8, 9, 4],
                    [7, 6, 5]]

```java
int[][] spiralNumbers(int n) {
    int[][] result = new int[n][n];
    int i=0;
    int j=0;
    int num = 1;
    int index = 0;

    while(true){

        result[i][j]=num;

        if(num==(n*n)){
            break;
        }

        if(index == 0){
            if(j==n-1 || result[i][j+1]!=0){
                index = 1;
            }else{
                j++;
                num++;
            }

        }else if(index == 1){

            if(i==n-1 || result[i+1][j]!=0){
                index = 2;
            }else{
               i++;
                num++;
            }

        }else if(index == 2){

            if(j==0 || result[i][j-1]!=0){
                index = 3;
            }else{
                j--;
                num++;
            }
        }else if(index == 3){

            if(i==0 || result[i-1][j]!=0){
                index = 0;
            }else{
                i--;
                num++;
            }
        }
    }
    return result;
}
```
