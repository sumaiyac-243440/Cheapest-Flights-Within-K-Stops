class Solution {
public:
    int findCheapestPrice(int n, vector<vector<int>>& flights, int src, int dst, int k) {

        vector<vector<pair<int,int>>> adj(n);

        for (auto &e : flights) {
            adj[e[0]].push_back({e[1], e[2]});
        }

        vector<int> dist(n, INT_MAX);

        queue<vector<int>> q;
        q.push({0, src, 0});

        dist[src] = 0;

        while (!q.empty()) {

            int stops = q.front()[0];
            int node = q.front()[1];
            int cost = q.front()[2];
            q.pop();

            if (stops > k)
                continue;

            for (auto &it : adj[node]) {

                int next = it.first;
                int price = it.second;

                if (cost + price < dist[next]) {

                    dist[next] = cost + price;
                    q.push({stops + 1, next, dist[next]});
                }
            }
        }

        if (dist[dst] == INT_MAX)
            return -1;

        return dist[dst];
    }
};
