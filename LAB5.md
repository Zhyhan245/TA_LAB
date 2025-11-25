### Лістинг 3.1 – код реалізації алгоритму Пріма.
```cpp
#include <iostream>
#include <cstring>
using namespace std;

#define INF 9999999
#define V 8

int G[V][V] = {
    {INF, 2, 5, INF, INF, INF, 1, INF},
    {2, INF, INF, 3, INF, INF, INF, INF},
    {5, INF, INF, 5, 2, 4, 4, INF},
    {INF, 3, 5, INF, 9, 5, 9, INF},
    {INF, INF, 2, 9, INF, 3, INF, INF},
    {INF, INF, 4, 5, 3, INF, INF, 1},
    {1, INF, 4, 9, INF, INF, INF, 6},
    {INF, INF, INF, INF, INF, 1, 6, INF}
};

int main() {
    int no_edge = 0;
    int selected[V];

    memset(selected, false, sizeof(selected));

    selected[0] = true;

    int x, y;

    cout << "Edge : Weight\n";

    while (no_edge < V - 1) {
        int min = INF;
        x = 0;
        y = 0;

        for (int i = 0; i < V; i++) {
            if (selected[i]) {
                for (int j = 0; j < V; j++) {
                    if (!selected[j] && G[i][j] < min) {
                        min = G[i][j];
                        x = i;
                        y = j;
                    }
                }
            }
        }

        cout << x + 1 << " - " << y + 1 << " : " << G[x][y] << endl;
        selected[y] = true;
        no_edge++;
    }

    return 0;
}


### Лістинг 5.1 – код реалізації алгоритму Крускала.
```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

#define edge pair<int,int>

class Graph {
private:
    vector<pair<int, edge>> G; 
    vector<pair<int, edge>> T; 
    int parent[8];

public:
    Graph() {
        for (int i = 0; i < 8; i++) parent[i] = i;
    }

    void Add(int u, int v, int w) {
        G.push_back({w, {u, v}});
    }

    int find_set(int v) {
        return (v == parent[v]) ? v : parent[v] = find_set(parent[v]);
    }

    void union_set(int a, int b) {
        parent[a] = b;
    }

    void kruskal() {
        sort(G.begin(), G.end());
        for (auto &e : G) {
            int u = e.second.first;
            int v = e.second.second;
            int w = e.first;
            int set_u = find_set(u);
            int set_v = find_set(v);
            if (set_u != set_v) {
                T.push_back(e);
                union_set(set_u, set_v);
            }
        }
        for (auto &e : T) {
            cout << (char)('a' + e.second.first)
                 << " - "
                 << (char)('a' + e.second.second)
                 << " : " << e.first << endl;
        }
    }
};

int main() {
    Graph g;

    g.Add(0, 6, 1); 
    g.Add(5, 7, 1); 
    g.Add(0, 1, 2); 
    g.Add(2, 4, 2); 
    g.Add(1, 3, 3); 
    g.Add(4, 5, 3); 
    g.Add(2, 5, 4); 
    g.Add(2, 6, 4); 
    g.Add(0, 2, 5); 
    g.Add(2, 3, 5); 
    g.Add(3, 5, 5);
    g.Add(6, 7, 6);
    g.Add(3, 4, 9); 
    g.Add(3, 6, 9); 

    g.kruskal();
    return 0;
}
