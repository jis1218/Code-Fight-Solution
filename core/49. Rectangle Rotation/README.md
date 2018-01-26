```java
int rectangleRotation(int a, int b) {
    
    int sero = 0;
    int garo = 0;
    
    for(int i=0; i<=a; i++){
        if(i*Math.sqrt(2)>a){
            garo = i;
            System.out.println(garo);
            break;
        }  
    }
    
    for(int j=0; j<=b; j++){
        if(j*Math.sqrt(2)>b){
            sero = j;
            System.out.println(sero);
            break;
        }
    }
    int result = 0;
    if((garo+sero)%2==0){
        result = garo*sero + (garo-1)*(sero-1);
    }else{
        result = garo*sero + (garo-1)*(sero-1) - 1;
    }
    
    return result;
}
```