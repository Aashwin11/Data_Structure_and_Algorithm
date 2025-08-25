class Solution {
public:
    vector<int> findDiagonalOrder(vector<vector<int>>& mat) {
        const int r=mat.size(), c=mat[0].size();
        vector<int> ans(r*c);
        bool flip=0;

        for (int d=0, idx=0; d < r+c-1; d++, flip=!flip) {
            if (!flip) {// go NE
                for (int i=min(d, r-1), j=d-i; i>=0 && j<c; i--, j++) 
                    ans[idx++]=mat[i][j];
            } 
            else {// go SW
                for (int j=min(d, c-1), i=d-j; j>=0 && i<r; i++, j--) {
                    ans[idx++]=mat[i][j];
                }
            }
        }
        return ans;
    }
};
