You are given a string s of characters that contains at least n numbers (here, a number is defined as a consecutive series of digits, where any character immediately to the left and right of the series are not digits). The numbers may contain leading zeros, but it is guaranteed that each number has at least one non-zero digit in it.

Your task is to find the nth number and return it as a string without leading zeros.

```java
String nthNumber(String s, int n) {
  Pattern pattern = Pattern.compile(
    "(?:\\D*(?:[0]*(\\d+)\\D*)){" + n + "}(\\D*\\d*\\D*)*"
  );

  Matcher matcher = pattern.matcher(s);
  matcher.matches();
  return matcher.group(1);
}
```

##### matcher()와 find()의 차이는
##### matcher()는 완전 정확한 것을 찾아주고
##### find()는 substring까지 찾아준다는 것이다.

```java
	static String nthNumber(String s) {
		  Pattern pattern = Pattern.compile("(?:\\D*(?:[0]*(\\d+))\\D*\\s*){4}");
		//Pattern pattern = Pattern.compile("(\\d\\d)\\1");

		  Matcher matcher = pattern.matcher(s);
		  matcher.find();
		  System.out.println(matcher.groupCount());
		  for(int i=0; i<=matcher.groupCount(); i++){
			  System.out.println(matcher.group(i));
		  }
		  return matcher.group(0);
		}
	
	static String nthNumber(String s, int n) {
		  Pattern pattern = Pattern.compile(
		    "(?:\\D*(?:[0]*(\\d+)\\D*)){1}(\\D*\\d*\\D*)*"
		  );

		  Matcher matcher = pattern.matcher(s);
		  matcher.matches();
		  System.out.println(matcher.groupCount());
		  System.out.println(matcher.group(0));
		  for(int i=0; i<=matcher.groupCount(); i++){
			  System.out.println("matcher.group("+ i + ") = " + matcher.group(i));
		  }
		  return matcher.group(1);
		}
```

##### 다른 풀이
```java
String nthNumber(String s, int n) {
  Pattern pattern = Pattern.compile(
    "(?:[^0-9]*[0-9]+){"+(n-1)+"}[^1-9]+([0-9]+).*"
  );

  Matcher matcher = pattern.matcher(s);
  matcher.matches();
  return matcher.group(1);
}

String nthNumber(String s, int n) {
  Pattern pattern = Pattern.compile(
    (n<=1?"":".*?(?:.*?\\d+){"+(n-1)+"}")+".*?0*(\\d+).*"
  );

  Matcher matcher = pattern.matcher(s);
  matcher.matches();
  return matcher.group(1);
}
```