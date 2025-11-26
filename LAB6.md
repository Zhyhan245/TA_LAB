Лістинг 6.1 – Код реалізації алгоритму
 ```cpp
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

Лістинг 6.2 – Код реалізації алгоритму

#include <stdio.h>
#define INF 1000000000
#define N 8

int main() {
    int W[N][N] = {
        {0,   2,   5,   INF, INF, INF, 1,   INF},
        {2,   0,   INF, 3,   INF, INF, INF, INF},
        {5,   INF, 0,   INF, 2,   4,   4,   INF},
        {INF, 3,   5,   0,   9,   5,   9,   INF},
        {INF, INF, 2,   9,   0,   3,   INF, INF},
        {INF, INF, 4,   5,   3,   0,   INF, 1},
        {1,   INF, 4,   9,   INF, INF, 0,   6},
        {INF, INF, INF, INF, INF, 1,   6,   0}
    };

    int D[N][N];

    for (int i = 0; i < N; i++)
        for (int j = 0; j < N; j++)
            D[i][j] = W[i][j];

    for (int k = 0; k < N; k++) {
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < N; j++) {
                if (D[i][k] + D[k][j] < D[i][j]) {
                    D[i][j] = D[i][k] + D[k][j];
                }
            }
        }
    }

    printf("Final matrix D:\\n");
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < N; j++) {
            if (D[i][j] >= INF)
                printf("INF ");
            else
                printf("%3d ", D[i][j]);
        }
        printf("\n");
    }

    return 0;
}



