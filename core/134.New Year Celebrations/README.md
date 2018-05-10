Your course lies west of your current location and crosses several time zones. The pilot told you the exact schedule: it is known that you will take off at takeOffTime, and in minutes[i] after takeoff you will cross the ith border between time zones. After crossing each border you will have to set your wrist watch one hour earlier (every second matters to you, so you can't let your watch show incorrect time). It is guaranteed that you won't cross the IDL (i.e. after crossing each time zone border your current time will be set one hour back).
You've been thinking about this situation and realized that it might be a good opportunity to celebrate New Year's Day more than once, i.e. each time your wrist watch shows 00:00. Assuming that you set your watch immediately after the border is crossed, how many times will you be able to celebrate this New Year's Day with a nice bottle of champagne? Note that the answer should include celebrations both in mid-air and on the ground (it doesn't matter if the plane landed in the last time zone before the midnight or not, you'll not let the last opportunity to celebrate New Year slip through your fingers).
Example
For takeOffTime = "23:35" and minutes = [60, 90, 140],
the output should be
newYearCelebrations(takeOffTime, minutes) = 3.
Here is the list of events by the time zones:
initial time zone: 
at 23:35 your flight starts;
at 00:00 you celebrate New Year for the first time;
at 00:35 (60 minutes after the take off) you cross the first border;
time zone -1: 
at 23:35 you cross the border (00:35 by your initial time zone);
at 00:00 you celebrate New Year for the second time (01:00 by your initial time zone);
at 00:05 (90 minutes after the take off) you cross the second border;
time zone -2: 
at 23:05 you cross the border;
at 23:55 (140 minutes after the take off) you cross another border;
time zone -3: 
at 22:55 you cross the border;
at 00:00 you celebrate New Year for the third time.
Thus, the output should be 3. That's a lot of champagne!
```java
int newYearCelebrations(String takeOffTime, int[] minutes) {
    
    int cnt = 0;
    int realTime[] = new int[minutes.length];
    int min = timeCal(takeOffTime);
    int localTime[] = new int[minutes.length];
    
    if(minutes.length>0){
        realTime[0] = min+minutes[0];
        for(int i=0; i<minutes.length-1; i++){            
            localTime[i] = min+minutes[i]-60*(i+1); 
            realTime[i+1] = localTime[i]+minutes[i+1]-minutes[i];
        }
        localTime[minutes.length-1] = min+minutes[minutes.length-1]-60*minutes.length;

        if(min<=1440 && realTime[0]>=1440) cnt++;
    
        for(int i=0; i<minutes.length-1; i++){
            if(realTime[i+1]>=1440 && localTime[i]<=1440) cnt++;
        }   
    
        if(localTime[minutes.length-1]<=1440) cnt++;
    }else{
        if(min<=1440) return 1;
    }    
    
    return cnt;
    
}

int timeCal(String time){
    int[] times = new int[2];
    times[0] = Integer.parseInt(time.split(":")[0]);
    if(times[0]==0){
        times[0] = 24;
    }
    times[1] = Integer.parseInt(time.split(":")[1]);
    
    return 60*times[0]+times[1];
}
```

##### 다른 짧은 풀이
```java
int newYearCelebrations(String takeOffTime, int[] minutes) {
    String[] s = takeOffTime.split(":");
    int time = Integer.parseInt(s[1]) + 60*Integer.parseInt(s[0]) + 2*60*24;
    int start = time;
    int count = 0;
    int min = start;
    for (int i = 0; i < minutes.length; i++) {
        int current = (time-1)/(60*24);
        time = start + minutes[i] - 60*i;
        count+=(time/(60*24) - current);
        time -= 60;
        if (time < min)
            min = time;
    }
    if ((min-1)/(60*24) == (time-1)/(60*24))
        count++;
    return count;
}
```