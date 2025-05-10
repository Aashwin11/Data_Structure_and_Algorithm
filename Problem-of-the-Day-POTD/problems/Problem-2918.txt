class Solution {
public:
    long long minSum(vector<int>& nums1, vector<int>& nums2) {
        ios_base::sync_with_stdio(false);
        cin.tie(0);
        cout.tie(0);

        long long sum1 = 0, sum2 = 0;
        int zeros1 = 0, zeros2 = 0;

        for (int n : nums1) {
            if (n == 0) zeros1++;
            sum1 += n;
        }

        for (int n : nums2) {
            if (n == 0) zeros2++;
            sum2 += n;
        }

        if (zeros1 == 0 && zeros2 == 0) {
            return sum1 == sum2 ? sum1 : -1;
        } else if (zeros1 == 0) {
            return sum2 + zeros2 <= sum1 ? sum1 : -1;
        } else if (zeros2 == 0) {
            return sum1 + zeros1 <= sum2 ? sum2 : -1;
        }

        return max(sum1 + zeros1, sum2 + zeros2);
    }
};
