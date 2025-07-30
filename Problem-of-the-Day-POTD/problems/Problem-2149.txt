#include <vector>
#include <algorithm>

class Solution {
public:
    int longestSubarray(std::vector<int>& nums) {
        if (nums.empty()) {
            return 0;
        }

        // 1. Find the maximum value in the array.
        int maxVal = 0;
        for (int num : nums) {
            if (num > maxVal) {
                maxVal = num;
            }
        }
        
        // 2. Find the length of the longest subarray of maxVal.
        int maxLen = 0;
        int currentLen = 0;
        
        for (int num : nums) {
            if (num == maxVal) {
                currentLen++;
            } else {
                maxLen = std::max(maxLen, currentLen);
                currentLen = 0;
            }
        }
        
        // 3. Final check for a trailing streak.
        return std::max(maxLen, currentLen);
    }
};
