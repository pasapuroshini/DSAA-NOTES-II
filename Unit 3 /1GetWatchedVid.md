```
import java.util.*;

class Solution {
    public List<String> watchedVideosByFriends(List<List<String>> watchedVideos, int[][] friends, int id, int level) {
        int n = friends.length;
        boolean[] visited = new boolean[n];
        Queue<Integer> queue = new LinkedList<>();
        queue.offer(id);
        visited[id] = true;
        
        // BFS to find level-k friends
        while (level-- > 0) {
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                int current = queue.poll();
                for (int f : friends[current]) {
                    if (!visited[f]) {
                        visited[f] = true;
                        queue.offer(f);
                    }
                }
            }
        }

        // Count video frequencies from people at level k
        Map<String, Integer> freqMap = new HashMap<>();
        while (!queue.isEmpty()) {
            int person = queue.poll();
            for (String video : watchedVideos.get(person)) {
                freqMap.put(video, freqMap.getOrDefault(video, 0) + 1);
            }
        }

        // Sort by frequency, then by name
        List<String> result = new ArrayList<>(freqMap.keySet());
        result.sort((a, b) -> {
            int freqCompare = freqMap.get(a) - freqMap.get(b);
            return freqCompare != 0 ? freqCompare : a.compareTo(b);
        });

        return result;
    }
}

```
