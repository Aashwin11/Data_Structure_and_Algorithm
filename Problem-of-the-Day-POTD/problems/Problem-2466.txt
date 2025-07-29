class Solution {
public:
    vector<int> smallestSubarrays(vector<int>& nums) {
        int len = nums.size();
        vector<int> res(len, 1);
        for (int i = 0; i < len; ++i) {
            int x = nums[i];
            res[i] = 1;
            int j = i - 1;
            while (j >= 0 && (nums[j] | x) != nums[j]) {
                res[j] = i - j + 1;
                nums[j] |= x;
                --j;
            }
        }
        return res;
    }
};
