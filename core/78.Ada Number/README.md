##### 정규식 공부

(?=X) X 앞으로 기준
```java
String b = "12#10001";
for(String str : b.split("(.{1}(?=#))")){
			System.out.println(str);
		}
```
##### 결과는 1, #10001

(?!X) X 앞으로 기준이나 그 문자를 제외한 나머지
