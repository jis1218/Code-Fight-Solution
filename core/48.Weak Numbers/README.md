```java
int[] weakNumbers(int n) {
    
    int[] divisor = new int[n];
    int[] weakness = new int[n];
    Arrays.fill(divisor, 1);
    
    for(int i=2; i<=n; i++){             
        for(int j=2; j<=i; j++){            
            if(i%j==0){                
                divisor[i-1]++;                
            }            
        }        
    }
    
    for(int i=0; i<n; i++){
        for(int j=0; j<i; j++){
            if(divisor[j]>divisor[i]){
                weakness[i]++;
            }
        }
    }
    int max=0;
    int result = 0;
    
    for(int i=0; i<n; i++){
        if(weakness[i]>max){
            max = weakness[i];
        }
    }
    
    for(int i=0; i<n; i++){
        if(weakness[i]==max){
            result++;
        }
    }
    
    int[] answer = {max, result};
    
    return answer;
}
```
