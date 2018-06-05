Your Math teacher takes education very seriously, and hates it when a class is missed or canceled for any reason. He even made up the following rule: if a class is missed because of a holiday, the teacher will compensate for it with a makeup class after school.
You're given an array, daysOfTheWeek, with the weekdays on which your teacher's classes are scheduled, and holidays, representing the dates of the holidays throughout the academic year (from 1st of September in year to 31st of May in year + 1). How many times will you be forced to stay after school for a makeup class because of holiday conflicts in the current academic year?
For your convenience, here is the list of month lengths (from January to December, respectively):
Month lengths: 31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31.
Please note that in leap years February has 29 days.
Example
For year = 2015, daysOfTheWeek = [2, 3] and
holidays = ["11-04", "02-22", "02-23", "03-07", "03-08", "05-09"],
the output should be
missedClasses(year, daysOfTheWeek, holidays) = 3.
November 4th of 2015 is a Wednesday, February 23th of 2016 and March 8th of 2016 are Tuesdays, and the other holidays fall on Mondays. Classes are scheduled on Wednesdays and Tuesdays, so there will be only 3 missed classes.

```java
int missedClasses(int year, int[] daysOfTheWeek, String[] holidays) {
    SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd");
    Calendar cal = Calendar.getInstance();
    int cnt=0;
    
    for(String s : holidays){
        try{
            if(Integer.parseInt(s.substring(0,2))>=9 && Integer.parseInt(s.substring(0,2))<=12){
                cal.setTime(sdf.parse(year+"-"+s));
            }else{
                cal.setTime(sdf.parse((year+1)+"-"+s));
            }
            
            for(int i : daysOfTheWeek){
                if((i+1)%7==cal.get(Calendar.DAY_OF_WEEK)%7){
                    cnt++;
                    break;
                }
            }            
        }catch(ParseException e){            
        }
    }    
    return cnt;
}
```