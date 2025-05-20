class Solution {
public:
    bool isZeroArray(vector<int>& nums, vector<vector<int>>& queries) {
        vector<int> diff(nums.size() + 1, 0);
        for (const auto& q : queries) {
            diff[q[0]]++; // diff[l]++
            if (q[1] + 1 < nums.size())
                diff[q[1] + 1]--; // diff[r + 1]--
        }

        int cnt = 0;
        for (int i = 0; i < nums.size(); i++) {
            cnt += diff[i];
            if (nums[i] > cnt)
                return false;
        }
        return true;
    }
};
