static constexpr int mod=1e9+7, B30=(1<<30)%mod;
class Solution {
public:
    static int modPow(long long x, int exp){
        if (exp==0) return 1;
        long long y=(exp&1)?x:1;
        return modPow(x*x%mod, exp>>1)*y%mod;
    }
    static int pow2mod(int exp){
        if (exp<30) return 1<<exp;
        auto [q, r]=div(exp, 30);
        long long B=modPow(B30, q);
        return B*(1<<r)%mod;
    }
    static vector<int> productQueries(int n, vector<vector<int>>& queries) {
        const int m=queries.size();
        bitset<30> B(n);
        vector<int> exp2;
        for(int i=0; i<30; i++)
            if (B[i]) exp2.push_back(i);

        partial_sum(exp2.cbegin(), exp2.cend(), exp2.begin());

        vector<int> ans(m);
        for(int i=0; i<m; i++){
            const int s=queries[i][0], e=queries[i][1];
            const int exp=exp2[e]-((s==0)?0:exp2[s-1]);
            ans[i]=pow2mod(exp);
        }
        return ans;
    }
};
