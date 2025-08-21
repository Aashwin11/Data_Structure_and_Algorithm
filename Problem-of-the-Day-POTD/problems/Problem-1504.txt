class Solution {
public:
    int numSubmat(vector<vector<int>>& mat) {
        int r = mat.size(), c = mat[0].size(), ans = 0;
        vector<int> h(c);
        for (int i = 0; i < r; i++) {
            for (int j = 0; j < c; j++) h[j] = mat[i][j] ? h[j] + 1 : 0;
            vector<int> sum(c);
            stack<int> st;
            for (int j = 0; j < c; j++) {
                while (!st.empty() && h[st.top()] >= h[j]) st.pop();
                if (!st.empty()) {
                    int p = st.top();
                    sum[j] = sum[p] + h[j] * (j - p);
                } else {
                    sum[j] = h[j] * (j + 1);
                }
                st.push(j);
                ans += sum[j];
            }
        }
        return ans;
    }
};
