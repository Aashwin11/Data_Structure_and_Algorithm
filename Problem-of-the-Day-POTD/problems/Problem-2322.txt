#include <vector>
#include <numeric>
#include <algorithm>
#include <unordered_set>

class Solution {
public:
    std::vector<int> subtree_xor;
    std::vector<std::unordered_set<int>> descendants;
    std::vector<std::vector<int>> graph;

    void dfs(int node, int parent, const std::vector<int>& nums) {
        subtree_xor[node] = nums[node];
        descendants[node].insert(node);

        for (int neighbor : graph[node]) {
            if (neighbor != parent) {
                dfs(neighbor, node, nums);
                subtree_xor[node] ^= subtree_xor[neighbor];
                descendants[node].insert(descendants[neighbor].begin(), descendants[neighbor].end());
            }
        }
    }

    int minimumScore(std::vector<int>& nums, std::vector<std::vector<int>>& edges) {
        int n = nums.size();
        graph.assign(n, std::vector<int>());
        subtree_xor.assign(n, 0);
        descendants.assign(n, std::unordered_set<int>());

        for (const auto& edge : edges) {
            graph[edge[0]].push_back(edge[1]);
            graph[edge[1]].push_back(edge[0]);
        }

        dfs(0, -1, nums);

        int total_xor = subtree_xor[0];
        int min_score = INT_MAX;

        for (int i = 1; i < n; ++i) {
            for (int j = i + 1; j < n; ++j) {
                int xor_i = subtree_xor[i];
                int xor_j = subtree_xor[j];
                int val1, val2, val3;

                if (descendants[i].count(j)) { // j is in i's subtree
                    val1 = xor_j;
                    val2 = xor_i ^ xor_j;
                    val3 = total_xor ^ xor_i;
                } else if (descendants[j].count(i)) { // i is in j's subtree
                    val1 = xor_i;
                    val2 = xor_j ^ xor_i;
                    val3 = total_xor ^ xor_j;
                } else { // Independent subtrees
                    val1 = xor_i;
                    val2 = xor_j;
                    val3 = total_xor ^ xor_i ^ xor_j;
                }
                
                int score = std::max({val1, val2, val3}) - std::min({val1, val2, val3});
                min_score = std::min(min_score, score);
            }
        }

        return min_score;
    }
};
