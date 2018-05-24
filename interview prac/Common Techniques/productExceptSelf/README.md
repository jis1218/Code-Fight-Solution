
##### 3시간 고민 끝에 힌트 보고 풀었다. 핵심은 맨 처음 풀이처럼 O(N^2)로 하는 것이 아니라 미리 i가 빠진 모든 원소의 곱을 계산해주는 것이다. 그 계산법은 아래와 같다.
```java
int productExceptSelf(int[] nums, int m) {
    
    int[] prefix = new int[nums.length];
    int[] suffix = new int[nums.length];
    prefix[0] = 1;
    suffix[suffix.length-1] = 1;
    for(int i=1; i<nums.length; i++){
        prefix[i] = (prefix[i-1]*nums[i-1])%m;
        suffix[suffix.length-1-i] = (suffix[suffix.length-i]*nums[nums.length-i])%m;
    }
    int sum = 0;
    for(int i=0; i<nums.length; i++){
        sum += (prefix[i]*suffix[i])%m;
    }
    
    return sum%m;
}
```


##### 첫 풀이... time limit execution 에러 발생
```java
int productExceptSelf(int[] nums, int m) {
    int times = 0;
    int modulo[] = new int[nums.length];
    int index = 0;

    for(int i=0; i<nums.length; i++){
        modulo[i] = nums[i]%m;
        if(modulo[i]==0){
            times++;
            index = i;
            if(times>1) return 0;
        }
    }
    
    int sum = 0;
    for(int i=0; i<nums.length; i++){
        int gop = 1;
        for(int j=0; j<nums.length; j++){
            if(i!=j){
                gop *= modulo[j];
                if(gop>100000){
                    gop = gop%m;
                }
                
                if(gop==0) break;
            }
        }
        sum += gop;
        System.out.println(sum);
    }
    
    
    return sum%m;
    

}
```