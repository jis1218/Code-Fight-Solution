##### Union-find 알고리즘에 대해 알 수 있었음...

```java
import java.util.*;

class Solution {
    public int solution(int n, int[][] costs) {
        int answer = 0;
        
        int[] root = new int[n];
        
        for(int i=0; i<n; i++) {
            root[i] = i;
        }
        
        ArrayList<Edge> list = new ArrayList<>();
        for(int [] cost: costs) {
            list.add(new Edge(cost[0], cost[1], cost[2]));
        }
        
        Collections.sort(list);
        
        int sum = 0;
        
        for(Edge edge : list) {
            if(find(edge.V, root) != find(edge.U, root)) {
                union(edge.V, edge.U, root);
                sum += edge.distance;
            }            
        }
        
        return sum;
    }
    
    private int find(int node, int[] root) {
        if(node==root[node]) return node;
        return root[node] = find(root[node], root);
    }
    
    private void union(int node1, int node2, int[] root) {
        int a = find(node1, root);
        int b = find(node2, root);
        
        if(b>a) root[b] = a;
        else root[a] = b;
    }
    
    class Edge implements Comparable<Edge> {
        private int U;
        private int V;
        private int distance;
        
        Edge(int U, int V, int distance) {
            this.U = U;
            this.V = V;
            this.distance = distance;
        }
        
        @Override
        public int compareTo(Edge e) {
            return this.distance - e.distance;
        }
    }
}
```