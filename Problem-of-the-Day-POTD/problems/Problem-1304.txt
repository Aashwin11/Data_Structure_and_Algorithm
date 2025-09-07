class Solution {
public:
    vector<int> sumZero(int n) {
        vector<int> a(n);
        for (int i = 0; i < n; i++) {
            a[i] = ((n & 1) && i == n/2) ? 0 : (i < n/2 ? i + 1 : -(n - i));
        }
        return a;
    }
};
