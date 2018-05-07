You have been watching a video for some time. Knowing the total video duration find out what portion of the video you have already watched.
Example
For part = "02:20:00" and total = "07:00:00", the output should be
videoPart(part, total) = [1, 3].
You have watched 1 / 3 of the whole video.
##### 최대 공약수를 이용한 풀이
```java
int[] videoPart(String part, String total) {
    String partInt[] = part.split(":");
    String totalInt[] = total.split(":");
    
    int partSec = Integer.parseInt(partInt[0])*3600 + Integer.parseInt(partInt[1])*60 + Integer.parseInt(partInt[2]);
    int totalSec = Integer.parseInt(totalInt[0])*3600 + Integer.parseInt(totalInt[1])*60 + Integer.parseInt(totalInt[2]);
    
    int parts = partSec;
    int totals = totalSec;
    int remain = 0;
    while(true){
        remain = totals%parts;
        if(remain==0) break;
        totals = parts;
        parts = remain;
    }
    
    int result[] = new int[2];
    
    result[0] = partSec/parts;
    result[1] = totalSec/parts;
    
    return result;

}
```

##### 아래처럼 나눠지는 수를 다 탐색하는 방법도 있지만 for문을 2부터 작은 수까지 돌려야 하므로 좋은 방법은 아닌듯 하다.

```java
int parse(String s) {
    String[] t = s.split(":");
    return 3600 * Integer.parseInt(t[0]) + 60 * Integer.parseInt(t[1]) + Integer.parseInt(t[2]);
}

int[] videoPart(String part, String total) {
    int p = parse(part);
    int t = parse(total);
    
    for (int n = 2; n <= p && n <= t; ) {
        if (p % n != 0 || t % n != 0) {
            n++;
        } else {
            p /= n;
            t /= n;
        }
    }
    
    return new int[] { p, t };
}
```