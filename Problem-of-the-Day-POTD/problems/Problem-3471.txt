class Solution {
public:
    int numOfUnplacedFruits(vector<int>& fruits, vector<int>& baskets) {
        int n = baskets.size();
        int N = 1;
        while (N <= n) N <<= 1;

        vector<int> segTree(N << 1);
        for (int i = 0; i < n; ++i)
            segTree[N + i] = baskets[i];
        
        for (int i = N - 1; i > 0; --i)
            segTree[i] = max(segTree[2 * i], segTree[2 * i + 1]);

        int count = 0;
        for (int fruit : fruits) {
            int index = 1;
            if (segTree[index] < fruit) {
                count++;
                continue;
            }

            while (index < N) {
                if (segTree[2 * index] >= fruit)
                    index = 2 * index;
                else
                    index = 2 * index + 1;
            }

            segTree[index] = -1;
            while (index > 1) {
                index >>= 1;
                segTree[index] = max(segTree[2 * index], segTree[2 * index + 1]);
            }
        }
        return count;
    }
};
