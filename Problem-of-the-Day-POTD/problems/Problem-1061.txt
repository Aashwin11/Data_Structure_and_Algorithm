class Solution {
public:
    // DFS to find the smallest lex character in the component
    char dfs(unordered_map<char, vector<char>>& adj, char cur, vector<int>& vis) {
        vis[cur - 'a'] = 1;
        char minChar = cur;
        for (char neighbor : adj[cur]) {
            if (vis[neighbor - 'a'] == 0) {
                minChar = min(minChar, dfs(adj, neighbor, vis));
            }
        }
        return minChar;
    }

    string smallestEquivalentString(string s1, string s2, string baseStr) {
        int n = s1.length();
        unordered_map<char, vector<char>> adj;

        // Step 1: Build the equivalence graph
        for (int i = 0; i < n; ++i) {
            char u = s1[i];
            char v = s2[i];
            adj[u].push_back(v);
            adj[v].push_back(u);
        }

        // Step 2: Replace each character in baseStr with the smallest equivalent
        string result;
        for (char ch : baseStr) {
            vector<int> vis(26, 0);
            char minChar = dfs(adj, ch, vis);
            result.push_back(minChar);
        }

        return result;
    }
};
