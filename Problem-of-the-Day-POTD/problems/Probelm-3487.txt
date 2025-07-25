class Solution {
public:
    int maxSum(vector<int>& nums) {
        int M=*max_element(nums.begin(), nums.end());
        if (M<=0) return M;
        bitset<101> seen=0;
        int sum=0;
        for(int x: nums){
            if (x>=0 && !seen[x]){
                sum+=x;
                seen[x]=1;
            }
        }
        return sum;
    }
};
