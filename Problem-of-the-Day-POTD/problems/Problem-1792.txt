class Solution {
public:
    double maxAverageRatio(vector<vector<int>>& classes, int extraStudents) {

        auto gain = [](int p, int t) {
            return (double)(p + 1) / (t + 1) - (double)p / t;
        };

        priority_queue<tuple<double, int, int>> pq;
        for (auto& c : classes) {
            pq.push({gain(c[0], c[1]), c[0], c[1]});
        }

        while (extraStudents--) {
            auto [g, p, t] = pq.top();
            pq.pop();
            p++, t++;
            pq.push({gain(p, t), p, t});
        }

        double total = 0.0;
        while (!pq.empty()) {
            auto [g, p, t] = pq.top();
            pq.pop();
            total += (double)p / t;
        }
        
        return total / classes.size();
    }
};
