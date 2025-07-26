#include <vector>
#include <algorithm>

class Solution {
public:
    long long maxSubarrays(int n, std::vector<std::vector<int>>& conflictingPairs) {
        std::vector<std::vector<int>> right(n + 1);
        for (const auto& pair : conflictingPairs) {
            right[std::max(pair[0], pair[1])].push_back(std::min(pair[0], pair[1]));
        }

        long long ans = 0;
        std::vector<long long> left = {0, 0};
        std::vector<long long> bonus(n + 1, 0);

        for (int r = 1; r <= n; ++r) {
            for (int l_val : right[r]) {
                // Manually update top two values
                if (l_val > left[0]) {
                    left = {static_cast<long long>(l_val), left[0]};
                } else if (l_val > left[1]) {
                    left = {left[0], static_cast<long long>(l_val)};
                }
            }

            ans += r - left[0];
            
            if (left[0] > 0) {
                bonus[left[0]] += left[0] - left[1];
            }
        }
        
        long long max_bonus = 0;
        for(long long b : bonus) {
            max_bonus = std::max(max_bonus, b);
        }

        return ans + max_bonus;
    }
};
