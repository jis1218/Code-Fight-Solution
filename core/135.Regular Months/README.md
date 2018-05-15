In an effort to be more innovative, your boss introduced a strange new tradition: the first day of every month you're allowed to work from home. You like this rule when the day falls on a Monday, because any excuse to skip rush hour traffic is great!
You and your colleagues have started calling these months regular months. Since you're a fan of working from home, you decide to find out how far away the nearest regular month is, given that the currMonth has just started.
For your convenience, here is a list of month lengths (from January to December, respectively):
Month lengths: 31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31.
Please, note that in leap years February has 29 days.
Example
For currMonth = "02-2016", the output should be
regularMonths(currMonth) = "08-2016".
February of 2016 year is regular, but it doesn't count since it has started already, so the next regular month is August of 2016 - which is the answer.

```java
String regularMonths(String currMonth) {
    
    SimpleDateFormat sdf = new SimpleDateFormat("dd-MM-yyyy");
    Calendar cal = Calendar.getInstance();
    try{
        cal.setTime(sdf.parse("01-"+currMonth));
    }catch(ParseException e){
    }
    
    while(true){
        cal.add(Calendar.MONTH, 1);
        if(cal.get(Calendar.DAY_OF_WEEK)==2){
            break;
        }
    }   
    
    return sdf.format(cal.getTime()).substring(3);

}
```

```java
String regularMonths(String currMonth) {
    String[] now = currMonth.split("-");
    Calendar c = new GregorianCalendar(Integer.parseInt(now[1]), Integer.parseInt(now[0]), 1);
    while(c.get(Calendar.DAY_OF_WEEK)!=Calendar.MONDAY)
        c.add(Calendar.MONTH, 1);
    int m = c.get(Calendar.MONTH)+1;
    int y = c.get(Calendar.YEAR);
    System.out.println(c.get(Calendar.DAY_OF_WEEK));
    return String.format("%02d",m) + "-" + y;
}
```

