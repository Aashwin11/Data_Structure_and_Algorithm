class Solution {
public:
    int maxTaskAssign(vector<int>& tasks, vector<int>& workers, int pills, int strength) {
        int left = 0, right = min(tasks.size(), workers.size());

        sort(tasks.begin(), tasks.end());
        sort(workers.begin(), workers.end());

        while(left < right) {
            int mid = (left + right + 1) / 2;
            int usedPills = 0;
            multiset<int> workersFree(workers.end() - mid, workers.end());

            bool canAssign = true;
            for(int i = mid - 1; i >= 0; --i) {
                auto it = prev(workersFree.end());

                if(*it < tasks[i]) {
                    it = workersFree.lower_bound(tasks[i] - strength);
                    if(it == workersFree.end()) {
                        canAssign = false;
                        break;
                    }
                    ++usedPills;
                    if(usedPills > pills) {
                        canAssign = false;
                        break;
                    }
                }
                workersFree.erase(it);
            }

            if(canAssign)
                left = mid;
            else
                right = mid - 1;
        }
        return left;
    }
};
