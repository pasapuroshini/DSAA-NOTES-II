# DIJKSTRA 2 VARIATIONS _____!!!


```
import java.util.*;

// Class to store pairs of (distance, node)
class Pair {
    int distance;
    int node;

    Pair(int distance, int node) {
        this.distance = distance;
        this.node = node;
    }
}

class Solution {
    // Dijkstra's algorithm function
    static int[] dijkstra(int V, ArrayList<ArrayList<ArrayList<Integer>>> adj, int S) {
        PriorityQueue<Pair> pq = new PriorityQueue<>((x, y) -> x.distance - y.distance);

        int[] dist = new int[V];
        for (int i = 0; i < V; i++) {
            dist[i] = (int) 1e9; // Initialize all distances as infinity
        }

        dist[S] = 0;
        pq.add(new Pair(0, S));

        while (pq.size() != 0) {
            int dis = pq.peek().distance;
            int node = pq.peek().node;
            pq.remove();

            for (int i = 0; i < adj.get(node).size(); i++) {
                int edgeWeight = adj.get(node).get(i).get(1);
                int adjNode = adj.get(node).get(i).get(0);

                if (dis + edgeWeight < dist[adjNode]) {
                    dist[adjNode] = dis + edgeWeight;
                    pq.add(new Pair(dist[adjNode], adjNode));
                }
            }
        }

        return dist;
    }

    // Main method to test the Dijkstra function
    public static void main(String[] args) {
        int V = 4; // Number of vertices
        int S = 0; // Source vertex

        // Initialize adjacency list
        ArrayList<ArrayList<ArrayList<Integer>>> adj = new ArrayList<>();
        for (int i = 0; i < V; i++) {
            adj.add(new ArrayList<>());
        }

        // Add edges: (from, to, weight)
        adj.get(0).add(new ArrayList<>(Arrays.asList(1, 4)));
        adj.get(0).add(new ArrayList<>(Arrays.asList(2, 1)));
        adj.get(2).add(new ArrayList<>(Arrays.asList(1, 2)));
        adj.get(1).add(new ArrayList<>(Arrays.asList(3, 1)));
        adj.get(2).add(new ArrayList<>(Arrays.asList(3, 5)));

        int[] result = dijkstra(V, adj, S);

        System.out.println("Shortest distances from source node " + S + ":");
        for (int i = 0; i < result.length; i++) {
            System.out.println("Node " + i + " → " + result[i]);
        }
    }
}

```






```
import java.util.*;

class Pair {
    int distance, node;

    Pair(int distance, int node) {
        this.distance = distance;
        this.node = node;
    }
}

public class Solution {
    
    public static int[] dijkstra(int V, ArrayList<ArrayList<ArrayList<Integer>>> adj, int S, int[] parent) {
        PriorityQueue<Pair> pq = new PriorityQueue<>((x, y) -> x.distance - y.distance);
        int[] dist = new int[V];
        Arrays.fill(dist, (int) 1e9);
        dist[S] = 0;
        pq.add(new Pair(0, S));
        parent[S] = -1;  // Source has no parent

        while (!pq.isEmpty()) {
            int dis = pq.peek().distance;
            int node = pq.peek().node;
            pq.remove();

            for (int i = 0; i < adj.get(node).size(); i++) {
                int edgeWeight = adj.get(node).get(i).get(0); // weight
                int adjNode = adj.get(node).get(i).get(1);     // destination

                if (dis + edgeWeight < dist[adjNode]) {
                    dist[adjNode] = dis + edgeWeight;
                    parent[adjNode] = node; // update parent
                    pq.add(new Pair(dist[adjNode], adjNode));
                }
            }
        }
        return dist;
    }

    // Function to print path from source to destination
    public static void printPath(int[] parent, int dest) {
        List<Integer> path = new ArrayList<>();
        int curr = dest;
        while (curr != -1) {
            path.add(curr);
            curr = parent[curr];
        }
        Collections.reverse(path);
        System.out.print("Shortest Path: ");
        for (int node : path) {
            System.out.print(node + " ");
        }
        System.out.println();
    }

    public static void main(String[] args) {
        int V = 6;  // Number of vertices
        int S = 0;  // Source node
        int D = 5;  // Destination node (change as needed)

        // Creating the graph
        ArrayList<ArrayList<ArrayList<Integer>>> adj = new ArrayList<>();
        for (int i = 0; i < V; i++) adj.add(new ArrayList<>());

        // Add edges (format: weight, node)
        // Example graph
        adj.get(0).add(new ArrayList<>(Arrays.asList(2, 1))); // edge 0 -> 1 with weight 2
        adj.get(0).add(new ArrayList<>(Arrays.asList(4, 2))); // edge 0 -> 2 with weight 4
        adj.get(1).add(new ArrayList<>(Arrays.asList(1, 2))); // edge 1 -> 2 with weight 1
        adj.get(1).add(new ArrayList<>(Arrays.asList(7, 3))); // edge 1 -> 3 with weight 7
        adj.get(2).add(new ArrayList<>(Arrays.asList(3, 4))); // edge 2 -> 4 with weight 3
        adj.get(3).add(new ArrayList<>(Arrays.asList(1, 5))); // edge 3 -> 5 with weight 1
        adj.get(4).add(new ArrayList<>(Arrays.asList(2, 5))); // edge 4 -> 5 with weight 2

        int[] parent = new int[V];
        int[] dist = dijkstra(V, adj, S, parent);

        System.out.println("Shortest distance from source to destination (" + D + ") = " + dist[D]);
        printPath(parent, D);
    }
}
```

<img width="691" alt="Screenshot 2025-05-11 at 12 49 04 PM" src="https://github.com/user-attachments/assets/69db35ea-7f76-47bc-99b2-0aeba9a8ba71" />
