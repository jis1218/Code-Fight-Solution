You have a list of dishes. Each dish is associated with a list of ingredients used to prepare it. You want to group the dishes by ingredients, so that for each ingredient you'll be able to find all the dishes that contain it (if there are at least 2 such dishes).
Return an array where each element is a list with the first element equal to the name of the ingredient and all of the other elements equal to the names of dishes that contain this ingredient. The dishes inside each list should be sorted lexicographically. The result array should be sorted lexicographically by the names of the ingredients in its elements.
Example
For
  dishes = [["Salad", "Tomato", "Cucumber", "Salad", "Sauce"],
            ["Pizza", "Tomato", "Sausage", "Sauce", "Dough"],
            ["Quesadilla", "Chicken", "Cheese", "Sauce"],
            ["Sandwich", "Salad", "Bread", "Tomato", "Cheese"]]
the output should be
  groupingDishes(dishes) = [["Cheese", "Quesadilla", "Sandwich"],
                            ["Salad", "Salad", "Sandwich"],
                            ["Sauce", "Pizza", "Quesadilla", "Salad"],
                            ["Tomato", "Pizza", "Salad", "Sandwich"]]
For
  dishes = [["Pasta", "Tomato Sauce", "Onions", "Garlic"],
            ["Chicken Curry", "Chicken", "Curry Sauce"],
            ["Fried Rice", "Rice", "Onions", "Nuts"],
            ["Salad", "Spinach", "Nuts"],
            ["Sandwich", "Cheese", "Bread"],
            ["Quesadilla", "Chicken", "Cheese"]]
the output should be
  groupingDishes(dishes) = [["Cheese", "Quesadilla", "Sandwich"],
                            ["Chicken", "Chicken Curry", "Quesadilla"],
                            ["Nuts", "Fried Rice", "Salad"],
                            ["Onions", "Fried Rice", "Pasta"]]

##### 우여곡절 끝에 나온 풀이... 이렇게 푸는 것이 아닌 것 같지만 많은 것을 배웠다.
##### 1. ArrayList<String[]> 을 배열로 바꿔주는 방법
```java
String[][] arr = list.toArray(new String[0][0]); //new String[0][0]으로 하면 list의 크기에 따라 array의 크기를 조정해준다. new String[0][]로 해도 된다.
```

##### 2. Arrays.sort도 범위를 지정해줄 수 있다.
```java
Arrays.sort(s, 1, s.length);
```

##### 3. Hashtable 함수 중 keys()가 있는데 이는 Enumeration<>을 반환한다. 사용법은 다음과 같다. 키를 가져올 수 있다.
```java
for(Enumeration<String> s = table.keys(); s.hasMoreElements();){
        String str = s.nextElement();
        if(table.get(str).split(", ").length>1){
            list.add((str + ", " + table.get(str)).split(", "));
        }
    }
```

##### 4. Array 또는 list를 sorting하는 방법(옵션에 따라 오름차순, 내림차순 가능)
```java
Collections.sort(list,(a,b)->a[0].compareTo(b[0])); 
```

##### 최종 풀이
```java
String[][] groupingDishes(String[][] dishes) {
    // 해시테이블 생성
    Hashtable<String, String> table = new Hashtable<>();
    // 해시테이블에 키와 데이터 값을 넣어준다.
    for(int i=0; i<dishes.length; i++){
        for(int j=1; j<dishes[i].length; j++){
            if(table.get(dishes[i][j])!=null){
                table.put(dishes[i][j], table.get(dishes[i][j]) + ", " + dishes[i][0]);
            }else{
                table.put(dishes[i][j], dishes[i][0]);
            }
        }
    }
    int size = table.size();
    //ArrayList를 만들어 데이터값(String array)를 넣어준다.
    ArrayList<String[]> list = new ArrayList<>();
    for(Enumeration<String> s = table.keys(); s.hasMoreElements();){
        String str = s.nextElement();
        if(table.get(str).split(", ").length>1){
            list.add((str + ", " + table.get(str)).split(", "));
        }
    }
    
    //맨 앞에 key값만 빼고 오름차순 sorting
    for(String s[] : list){
        Arrays.sort(s, 1, s.length);
    }
    
    String[][] arr = list.toArray(new String[0][0]);
    
    //키값에 따라 sorting
    for(int i=0; i<arr.length-1; i++){
        int index = i;
        String temp = arr[i][0];
        for(int j=i+1; j<arr.length; j++){
            if(arr[j][0].compareTo(temp)<0){
                temp = arr[j][0];
                index = j;
            }
        }
        String[] tempArr = Arrays.copyOf(arr[index], arr[index].length);
        arr[index] = Arrays.copyOf(arr[i], arr[i].length);
        arr[i] = Arrays.copyOf(tempArr, tempArr.length);
    }    
    
    return arr;
}
```

##### 다른 사람의 풀이

##### 일단 나와 가장 비슷하게 푼 사람의 다른점은 key값에 따른 sorting을 다음과 같이 해줬다는 것이다.
```java
//다른 사람
Collections.sort(list,(a,b)->a[0].compareTo(b[0]));

//나
for(int i=0; i<arr.length-1; i++){
        int index = i;
        String temp = arr[i][0];
        for(int j=i+1; j<arr.length; j++){
            if(arr[j][0].compareTo(temp)<0){
                temp = arr[j][0];
                index = j;
            }
        }
        String[] tempArr = Arrays.copyOf(arr[index], arr[index].length);
        arr[index] = Arrays.copyOf(arr[i], arr[i].length);
        arr[i] = Arrays.copyOf(tempArr, tempArr.length);
    }
```

##### 다른 사람의 것을 참고한 풀이
```java
String[][] groupingDishes(String[][] dishes) {
    Hashtable<String, String> table = new Hashtable<>();
    for(int i=0; i<dishes.length; i++){
        for(int j=1; j<dishes[i].length; j++){
            if(table.get(dishes[i][j])!=null){
                table.put(dishes[i][j], table.get(dishes[i][j]) + ", " + dishes[i][0]);
            }else{
                table.put(dishes[i][j], dishes[i][0]);
            }
        }
    }
    int size = table.size();
    ArrayList<String[]> list = new ArrayList<>();
    for(Enumeration<String> s = table.keys(); s.hasMoreElements();){
        String str = s.nextElement();
        if(table.get(str).split(", ").length>1){
            list.add((str + ", " + table.get(str)).split(", "));
        }
    }
    
    for(String s[] : list){
        Arrays.sort(s, 1, s.length);
    }
    
    Collections.sort(list,(a,b)->a[0].compareTo(b[0]));   
    
    return list.toArray(new String[0][]);
}
```

##### 제일 많은 추천을 받은 사람의 풀이
```java
String[][] groupingDishes(String[][] dishes) {
    return Arrays.stream(dishes)
        .flatMap(d -> Arrays.stream(d).skip(1).map(i -> new AbstractMap.SimpleEntry(i, d[0])))
        .collect(Collectors.groupingBy(
            Map.Entry::getKey, TreeMap::new, Collectors.mapping(Map.Entry::getValue, Collectors.toList())))
        .entrySet()
        .stream()
        .filter(e -> e.getValue().size() > 1)
        .map(e -> Stream.concat(Stream.of(e.getKey()), e.getValue().stream().sorted()).toArray(String[]::new))
        .toArray(String[][]::new);
}
```