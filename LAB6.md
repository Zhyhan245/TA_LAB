Лістинг 6.1 – Код реалізації алгоритму
 import java.util.*;

public class DijkstraListing61 {

    public static class Node implements Comparable<Node> {
        int vertex;
        int dist;

        Node(int v, int d) {
            vertex = v;
            dist = d;
        }

        @Override
        public int compareTo(Node other) {
            return Integer.compare(this.dist, other.dist);
        }
    }

    public static void dijkstra(List<List<int[]>> G, int s) {

        int n = G.size();

        int[] pred = new int[n];
        int[] dist = new int[n];
        boolean[] visited = new boolean[n];

        PriorityQueue<Node> pq = new PriorityQueue<>();

        for (int v = 0; v < n; v++) {
            pred[v] = -1;
            dist[v] = (v == s ? 0 : Integer.MAX_VALUE);
        }

        pq.add(new Node(s, 0));

        while (!pq.isEmpty()) {

            Node node = pq.poll();
            int u = node.vertex;

            if (visited[u])
                continue;
            visited[u] = true;

            for (int[] edge : G.get(u)) {
                int v = edge[0];
                int w = edge[1];

                if (dist[v] > dist[u] + w) {
                    dist[v] = dist[u] + w;
                    pred[v] = u;

                    pq.add(new Node(v, dist[v]));
                }
            }
        }

        System.out.println("pred = " + Arrays.toString(pred));
        System.out.println("dist = " + Arrays.toString(dist));
    }

    public static void main(String[] args) {

        List<List<int[]>> G = new ArrayList<>();
        for (int i = 0; i < 5; i++)
            G.add(new ArrayList<>());

        G.get(0).add(new int[]{1, 4});
        G.get(0).add(new int[]{2, 2});

        G.get(1).add(new int[]{0, 4});
        G.get(1).add(new int[]{2, 5});
        G.get(1).add(new int[]{3, 10});

        G.get(2).add(new int[]{0, 2});
        G.get(2).add(new int[]{1, 5});
        G.get(2).add(new int[]{4, 3});

        G.get(3).add(new int[]{1, 10});
        G.get(3).add(new int[]{4, 4});

        G.get(4).add(new int[]{2, 3});
        G.get(4).add(new int[]{3, 4});

        dijkstra(G, 0);
    }
}
