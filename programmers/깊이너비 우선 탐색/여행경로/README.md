주어진 항공권을 모두 이용하여 여행경로를 짜려고 합니다. 항상 ICN 공항에서 출발합니다.

항공권 정보가 담긴 2차원 배열 tickets가 매개변수로 주어질 때, 방문하는 공항 경로를 배열에 담아 return 하도록 solution 함수를 작성해주세요.

제한사항
모든 공항은 알파벳 대문자 3글자로 이루어집니다.
주어진 공항 수는 3개 이상 10,000개 이하입니다.
tickets의 각 행 [a, b]는 a 공항에서 b 공항으로 가는 항공권이 있다는 의미입니다.
주어진 항공권은 모두 사용해야 합니다.
만일 가능한 경로가 2개 이상일 경우 알파벳 순서가 앞서는 경로를 return 합니다.
모든 도시를 방문할 수 없는 경우는 주어지지 않습니다.
입출력 예
tickets	return
[[ICN, JFK], [HND, IAD], [JFK, HND]]	[ICN, JFK, HND, IAD]
[[ICN, SFO], [ICN, ATL], [SFO, ATL], [ATL, ICN], [ATL,SFO]]	[ICN, ATL, ICN, SFO, ATL, SFO]

```java
import java.util.*;
class Solution {
    ArrayList<ArrayList<String>> list = new ArrayList<>();
    public String[] solution(String[][] tickets) {
        boolean visited[] = new boolean[tickets.length];
        ArrayList<String> route = new ArrayList<>();
        Arrays.fill(visited, false);
        route.add("ICN");
        for(int i=0; i<tickets.length; i++){            
            if(tickets[i][0].equals("ICN")){                
                visited[i]=true;
                helper(tickets, visited, tickets[i][1], new ArrayList<String>(route));
                visited[i]=false;
            }
        }       
        
        Collections.sort(list, new Comparator<ArrayList<String>>(){
            public int compare(ArrayList<String> list1, ArrayList<String> list2){
                StringBuilder s1 = new StringBuilder();
                StringBuilder s2 = new StringBuilder();
                for(String s : list1){
                    s1.append(s);
                }
                for(String s : list2){
                    s2.append(s);
                }
                return s1.toString().compareTo(s2.toString());
            }
        });  
        return list.get(0).toArray(new String[0]);
    }
    
    void helper(String[][] tickets, boolean visited[], String arrival, ArrayList<String> route){
        route.add(arrival);
        if(route.size()==tickets.length+1){
            list.add(new ArrayList<String>(route));
            return;
        } 
        for(int i=0; i<tickets.length; i++){
            if(!visited[i] && arrival.equals(tickets[i][0])){
                visited[i]=true;                
                helper(tickets, visited, tickets[i][1], new ArrayList<String>(route));
                visited[i]=false;                
            }
        }
    }    
}
```