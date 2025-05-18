class Solution {
public:
    const static int MOD = 1e9 + 7;
    int m, n;
    vector<int> validMasks;
    unordered_map<int, vector<int>> nextMasks;
    unordered_map<long long, int> memo;

    // Check if two columns (represented as integers) are compatible (no same color in same row)
    bool isCompatible(int a, int b) {
        for (int i = 0; i < m; ++i) {
            if ((a % 3) == (b % 3)) {
                return false;
            }
            a /= 3;
            b /= 3;
        }
        return true;
    }

    // Check if a column (represented as integer) is valid (no two adjacent cells same)
    bool isValid(int mask) {
        int prev = -1;
        for (int i = 0; i < m; ++i) {
            int cur = mask % 3;
            if (cur == prev) {
                return false;
            }
            prev = cur;
            mask /= 3;
        }
        return true;
    }

    void generateValidMasks() {
        int maxMask = pow(3, m);
        for (int mask = 0; mask < maxMask; ++mask) {
            if (isValid(mask)) {
                validMasks.push_back(mask);
            }
        }

        for (int mask1 : validMasks) {
            for (int mask2 : validMasks) {
                if (isCompatible(mask1, mask2)) {
                    nextMasks[mask1].push_back(mask2);
                }
            }
        }
    }

    int dfs(int col, int prevMask) {
        if (col == n)
            return 1;

        long long key = ((long long)col << 10) | prevMask;
        if (memo.count(key)) {
            return memo[key];
        }

        int res = 0;
        for (int next : nextMasks[prevMask]) {
            res = (res + dfs(col + 1, next)) % MOD;
        }

        return memo[key] = res;
    }

    int colorTheGrid(int m_, int n_) {
        m = m_;
        n = n_;
        generateValidMasks();

        int res = 0;
        for (int mask : validMasks) {
            res = (res + dfs(1, mask)) % MOD;
        }
        return res;
    }
};
