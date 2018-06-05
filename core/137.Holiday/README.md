John Doe likes holidays very much, and he was very happy to hear that his country's government decided to introduce yet another one. He heard that the new holiday will be celebrated each year on the xth week of month, on weekDay.
Your task is to return the day of month on which the holiday will be celebrated in the year yearNumber.
For your convenience, here are the lists of months names and lengths and the list of days of the week names.
Months: "January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December".
Months lengths: 31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31.
Days of the week: "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", "Sunday".
Please, note that in leap years February has 29 days.
Example
For x = 3, weekDay = "Wednesday", month = "November" and yearNumber = 2016, the output should be
holiday(x, weekDay, month, yearNumber) = 16.
The new holiday will be celebrated every November on the 3rd Wednesday of the month. In 2016 the 3rd Wednesday falls on the 16th of November.
For x = 5, weekDay = "Thursday", month = "November" and yearNumber = 2016, the output should be
holiday(x, weekDay, month, yearNumber) = -1.
There are only 4 Thursdays in November 2016.
```java
int holiday(int x, String weekDay, String month, int yearNumber) {
    
    Calendar cal = Calendar.getInstance();
    SimpleDateFormat sdf = new SimpleDateFormat("yyyyMMMWEEEEE");
    SimpleDateFormat sdf2 = new SimpleDateFormat("dd");
    SimpleDateFormat sdf3 = new SimpleDateFormat("MMM");
    
    try{
        cal.setTime(sdf.parse(yearNumber+month+"1"+weekDay));
        
        if(!month.substring(0,3).equals(sdf3.format(cal.getTime()))) x++;
        
        cal.setTime(sdf.parse(yearNumber+month+x+weekDay));       
        
        if(!sdf3.format(cal.getTime()).equals(month.substring(0,3))) return -1;
        else{
            return Integer.parseInt(sdf2.format(cal.getTime()));
        }
    }catch(ParseException e){
        e.printStackTrace();
    }
    
    return -1;
}
```