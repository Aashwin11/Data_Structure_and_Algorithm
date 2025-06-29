class Solution {
public:
    int numSubseq(vector<int>& nums, int target) {
        const int mod=1e9+7;
        if (!is_sorted(nums.begin(), nums.end()))
            sort(nums.begin(), nums.end());

        int n=nums.size();       
        vector<int> pow2mod(n+1, 1);
        for (int exp=1; exp<=n; exp++)
            pow2mod[exp]=(pow2mod[exp-1]<<1)%mod;
        
        int l=0, r=n-1;
        int ans=0;
        while(l<=r){
            if( nums[l]+nums[r]<=target){
                ans=(ans+pow2mod[r-l])%mod;
                l++;
            }
            else r--;
        }
        return ans;
    }
};
