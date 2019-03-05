HTML tables allow web developers to arrange data into rows and columns of cells. They are created using the <table> tag. Its content consists of one or more rows denoted by the <tr> tag. Further, the content of each row comprises one or more cells denoted by the <td> tag, and content within the <td> tags is what site visitors see in the table. For this task assume that tags have no attributes in contrast to real world HTML.

Some tables contain the <th> tag. This tag defines header cells, which shouldn't be counted as regular cells.

You are given a rectangular HTML table. Extract the content of the cell with coordinates (row, column).

If you are not familiar with HTML, check out this note.

Example

For table = "<table><tr><td>1</td><td>TWO</td></tr><tr><td>three</td><td>FoUr4</td></tr></table>", row = 0, and column = 1, the output should be
htmlTable(table, row, column) = "TWO".

##### 첫풀이
```java
	static String htmlTable(String table, int row, int column) {
		int index = 0;
		for(int i=0; i<row+1; i++){			
			index = table.indexOf("<tr>", index+1);
		}
		if(index==-1) return "No such cell";
		
		int index4 = table.indexOf("</tr>", index);
		table = table.substring(index, index4);
		System.out.println(table);
		
		int index2 = 0;
		for(int i=0; i<column+1; i++){
			index2 = table.indexOf("<td>", index2+1);
		}
		if(index2==-1) return "No such cell";
		
		int index3 = table.indexOf("</td>", index2);		
		
		return table.substring(index2+4, index3);
	}
```

##### 정규식을 사용한 풀이
```java
	static String htmlTable2(String table, int row, int column) {
		String pattern = "(<tr>.*?</tr>)";
		Pattern patterns = Pattern.compile(pattern);
		Matcher matcher = patterns.matcher(table);
		for(int i=0; i<row+1; i++){
			if(!matcher.find()) return "No such cell";
		}
		String pattern2 = "<td>(.*?)</td>";
		patterns = Pattern.compile(pattern2);
		matcher = patterns.matcher(matcher.group(0));
		for(int i=0; i<column+1; i++){
			if(!matcher.find()) return "No such cell";
		}
		return matcher.group(1);
	}
```
##### quantifiers에 3가지가 있다. Greedy와 Reluctant, Possessive
##### 그에 관한 설명 https://stackoverflow.com/questions/5319840/greedy-vs-reluctant-vs-possessive-quantifiers