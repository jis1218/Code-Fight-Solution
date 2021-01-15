```java
class Solution {
    public int[] deckRevealedIncreasing(int[] deck) {
        Arrays.sort(deck);
		int len = deck.length;
		ArrayList<Integer> list = new ArrayList<>();		
		LinkedList<Integer> link = new LinkedList<>();
		
		for(int i=0; i<len; i++){
			link.addLast(deck[i]);
		}
		
		while(link.size()>0){
			list.add(link.pollFirst());
			if(link.size()==0) break;
			int poll = link.pollFirst();			
			link.addLast(poll);
		}		
		
		int[] guide = IntStream.range(0, len).boxed()
				.sorted((a, b)-> list.get(a).compareTo(list.get(b))).mapToInt(i -> i).toArray();
		
		int[] answer = Arrays.stream(guide).boxed().mapToInt(i->deck[i]).toArray();
        
        return answer;
    }
}
```