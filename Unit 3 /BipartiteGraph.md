```
import java.util.*;

public class BipartiteCheck {
    
    // Function to check if the graph is bipartite
    public boolean isBipartite(int[][] graph) {
        int n = graph.length;
        int[] color = new int[n];
        Arrays.fill(color, -1);  // -1 means not colored yet

        for (int node = 0; node < n; node++) {
            if (color[node] == -1) {
                // Start BFS from this unvisited node
                if (!bfsCheck(graph, node, color)) {
                    return false;
                }
            }
        }

        return true;
    }

    // BFS function to color the graph and check bipartite condition
    private boolean bfsCheck(int[][] graph, int startNode, int[] color) {
        Queue<Integer> queue = new LinkedList<>();
        queue.offer(startNode);
        color[startNode] = 0; // Start coloring with color 0

        while (!queue.isEmpty()) {
            int currentNode = queue.poll();

            for (int neighbor : graph[currentNode]) {
                if (color[neighbor] == -1) {
                    // Assign opposite color to neighbor
                    color[neighbor] = 1 - color[currentNode];
                    queue.offer(neighbor);
                } else if (color[neighbor] == color[currentNode]) {
                    // Conflict: same color on both ends of an edge
                    return false;
                }
            }
        }

        return true;
    }

    // 🔽 Main function with example input
    public static void main(String[] args) {
        BipartiteCheck checker = new BipartiteCheck();

        // Example 1: NOT bipartite
        int[][] graph1 = {
            {1, 2, 3}, 
            {0, 2}, 
            {0, 1, 3}, 
            {0, 2}
        };
        System.out.println("Graph 1 is bipartite? " + checker.isBipartite(graph1)); // false

        // Example 2: Bipartite
        int[][] graph2 = {
            {1, 3}, 
            {0, 2}, 
            {1, 3}, 
            {0, 2}
        };
        System.out.println("Graph 2 is bipartite? " + checker.isBipartite(graph2)); // true
    }
}

```
