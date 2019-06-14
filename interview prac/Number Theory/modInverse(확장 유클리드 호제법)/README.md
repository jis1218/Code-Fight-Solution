```java
long modInverse(long n, long m) {
    //확장 유클리드 알고리즘을 사용해야 한다.
    
    if(n==0) return -1;
    
    long real_m = m;
    long real_n = n;
    
    long t1 = 0;
    long t2 = 1;
    long s1 = 1;
    long s2 = 0;
    
    while(true){
        if(n>m){
            long temp = n;
            n = m;
            m = temp;
        }  
        long q = m/n;
        m = m%n;    
        if(m==0){
            break;
        } 
        
        long temp_t = t1;
        t1 = t2;
        t2 = temp_t-t2*q;
        
        long temp_s = s1;
        s1 = s2;
        s2 = temp_s-s2*q;
        
    }
    if(n!=1) return -1;
    
    return t2<0?real_m+t2:t2;
}

```