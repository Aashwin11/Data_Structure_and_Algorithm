class Solution {
public:
    int maxCollectedFruits(vector<vector<int>>& fruits) {
        int n = fruits.size();
        int total = 0;

        for (int i = 0; i < n; ++i)
            total += fruits[i][i];

        vector<int> rightPath(3, 0);
        rightPath[0] = fruits[0][n - 1];

        vector<int> bottomPath(3, 0);
        bottomPath[0] = fruits[n - 1][0];

        int window = 2;

        for (int step = 1; step < n - 1; ++step) {
            vector<int> newRight(window + 2, 0);
            vector<int> newBottom(window + 2, 0);

            for (int dist = 0; dist < window; ++dist) {
                int left = dist - 1 >= 0 ? rightPath[dist - 1] : 0;
                int mid = rightPath[dist];
                int right = dist + 1 < rightPath.size() ? rightPath[dist + 1] : 0;
                newRight[dist] = max({left, mid, right}) + fruits[step][n - 1 - dist];

                left = dist - 1 >= 0 ? bottomPath[dist - 1] : 0;
                mid = bottomPath[dist];
                right = dist + 1 < bottomPath.size() ? bottomPath[dist + 1] : 0;
                newBottom[dist] = max({left, mid, right}) + fruits[n - 1 - dist][step];
            }

            rightPath = newRight;
            bottomPath = newBottom;

            if (window - n + 4 + step <= 1) window++;
            else if (window - n + 3 + step > 1) window--;
        }

        return total + rightPath[0] + bottomPath[0];
    }
};
