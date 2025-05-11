```
import java.util.*;

class Solution {
    static int[] bellman_ford(int V, ArrayList<ArrayList<Integer>> edges, int S, int[] parent) {
        int[] dist = new int[V];
        Arrays.fill(dist, (int) 1e8);
        Arrays.fill(parent, -1);  // For path tracking

        dist[S] = 0;

        // Relax all edges V-1 times
        for (int i = 0; i < V - 1; i++) {
            for (ArrayList<Integer> it : edges) {
                int u = it.get(0);
                int v = it.get(1);
                int wt = it.get(2);
                if (dist[u] != 1e8 && dist[u] + wt < dist[v]) {
                    dist[v] = dist[u] + wt;
                    parent[v] = u;
                }
            }
        }

        // Check for negative weight cycle
        for (ArrayList<Integer> it : edges) {
            int u = it.get(0);
            int v = it.get(1);
            int wt = it.get(2);
            if (dist[u] != 1e8 && dist[u] + wt < dist[v]) {
                return new int[]{-1};  // Negative cycle detected
            }
        }

        return dist;
    }

    static void printPath(int node, int[] parent) {
        List<Integer> path = new ArrayList<>();
        while (node != -1) {
            path.add(node);
            node = parent[node];
        }
        Collections.reverse(path);
        for (int i = 0; i < path.size(); i++) {
            System.out.print(path.get(i));
            if (i != path.size() - 1) System.out.print(" -> ");
        }
    }
}

public class tUf {
    public static void main(String[] args) {
        int V = 6;
        int S = 0;

        ArrayList<ArrayList<Integer>> edges = new ArrayList<>() {{
            add(new ArrayList<>(Arrays.asList(3, 2, 6)));
            add(new ArrayList<>(Arrays.asList(5, 3, 1)));
            add(new ArrayList<>(Arrays.asList(0, 1, 5)));
            add(new ArrayList<>(Arrays.asList(1, 5, -3)));
            add(new ArrayList<>(Arrays.asList(1, 2, -2)));
            add(new ArrayList<>(Arrays.asList(3, 4, -2)));
            add(new ArrayList<>(Arrays.asList(2, 4, 3)));
        }};

        int[] parent = new int[V];
        int[] dist = Solution.bellman_ford(V, edges, S, parent);

        if (dist.length == 1 && dist[0] == -1) {
            System.out.println("Negative weight cycle detected.");
        } else {
            for (int i = 0; i < V; i++) {
                System.out.print("Shortest distance to node " + i + " is " + dist[i]);
                System.out.print(" | Path: ");
                Solution.printPath(i, parent);
                System.out.println();
            }
        }
    }
}

```


<img width="575" alt="Screenshot 2025-05-11 at 2 42 46 PM" src="https://github.com/user-attachments/assets/9053f97b-fb8f-497b-86aa-d4c1b260d346" />
