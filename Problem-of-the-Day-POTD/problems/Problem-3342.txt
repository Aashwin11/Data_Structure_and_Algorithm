class Solution {
public:
    int minTimeToReach(vector<vector<int>>& moveTime) {
        int n = moveTime.size(), m = moveTime[0].size();
        vector<vector<bool>> vis(n, vector<bool>(m));
        priority_queue<pair<int, pair<int, pair<int, int>>>,
                       vector<pair<int, pair<int, pair<int, int>>>>, greater<>>
            pq;
        pq.push({0, {0, {0, 0}}});
        vis[0][0] = true;
        int dir[][2] = {{0, 1}, {1, 0}, {-1, 0}, {0, -1}};
        while (!pq.empty()) {
            auto [t, next] = pq.top();
            pq.pop();
            auto [move, cell] = next;
            auto [r, c] = cell;
            if (r == n - 1 && c == m - 1)
                return t;
            for (int i = 0; i < 4; i++) {
                int nr = r + dir[i][0], nc = c + dir[i][1];
                if (nr >= 0 && nc >= 0 && nr < n && nc < m && !vis[nr][nc]) {
                    vis[nr][nc] = true;
                    int time =
                        max(t, moveTime[nr][nc]) + (move % 2 == 0 ? 1 : 2);
                    pq.push({time, {move + 1, {nr, nc}}});
                }
            }
        }
        return -1;
    }
};
