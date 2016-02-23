Before Java 8, dealing with `DateTime` in Java suck. In my case, I had to deal with time from differen time zone, here is how I deal with it
```Java
...
//using only Java ulti
public Date parseString(String str, String format, TimeZone tz) throws ParseException {
  SimpleDateFormat sdf = null;
  if(format == null) {
    sdf = new SimpleDateFormat(DEFAULT_FORMAT_DATE);
  } else {
    sdf = new SimpleDateFormat(format);
  }
  if (tz != null) {sdf.setTimeZone(tz);}
  return sdf.parse(str);
}
...
// Data is created in different timezone (and different server) with the current server
Date createdTime = parseString("2015-12-08T05:44:00Z", "yyyy-MM-dd'T'HH:mm:ss'Z'", TimeZone.getTimeZone("JST"));
Date lastUpdatedTime = parseString("2015-12-08T05:44:00Z", "yyyy-MM-dd'T'HH:mm:ss'Z'", Calendar.getInstance().getTimeZone());
...
System.out.println(createdTime.after(lastUpdatedTime)); // true
```

In Java 8, you can use `ZoneDateTime` to deal with the situation above ( and ***many many more things***).

```Java
LocalDateTime datetime = LocalDateTime.of(2015, Month.DECEMBER, 08, 05, 44); 
ZonedDateTime createdTime = ZonedDateTime.of(datetime, "Asia/Tokyo"); 
ZonedDateTime lastUpdatedTime = ZonedDateTime.of(datetime, ZoneId.systemDefault()); 
System.out.println(createdTime.until(lastUpdatedTime, ChronoUnit.SECONDS) > 0); //true
```
