class Solution {
    static const int mod = 1e9 + 7;
    using ll = long long;
    vector<ll> fact, inv, invFact;

    void precompute(int n) {
        fact.assign(n + 1, 1);
        for (int i = 1; i <= n; i++)
            fact[i] = fact[i - 1] * i % mod;

        inv.assign(n + 1, 1);
        for (int i = 2; i <= n; i++)
            inv[i] = mod - (mod / i) * inv[mod % i] % mod;

        invFact.assign(n + 1, 1);
        for (int i = 1; i <= n; i++)
            invFact[i] = invFact[i - 1] * inv[i] % mod;
    }

public:
    int countBalancedPermutations(const string& s) {
        int n = s.size(), sum = 0;
        for (char c : s) sum += c - '0';
        if (sum % 2 == 1) return 0;

        precompute(n);
        int halfSum = sum / 2, halfLen = n / 2;
        vector<vector<int>> dp(halfSum + 1, vector<int>(halfLen + 1));
        dp[0][0] = 1;

        vector<int> digits(10);
        for (char c : s) {
            int d = c - '0';
            digits[d]++;
            for (int i = halfSum; i >= d; i--)
                for (int j = halfLen; j > 0; j--)
                    dp[i][j] = (dp[i][j] + dp[i - d][j - 1]) % mod;
        }

        ll res = dp[halfSum][halfLen];
        res = res * fact[halfLen] % mod * fact[n - halfLen] % mod;
        for (int i : digits)
            res = res * invFact[i] % mod;
        return res;
    }
};
