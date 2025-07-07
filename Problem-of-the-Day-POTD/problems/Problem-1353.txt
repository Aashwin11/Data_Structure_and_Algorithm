class Solution {
    int findNext(vector<int>& nextDay, int day) {
        if (nextDay[day] != day) {
            nextDay[day] = findNext(nextDay, nextDay[day]);
        }
        return nextDay[day];
    }

public:
    int maxEvents(vector<vector<int>>& events) {
        sort(events.begin(), events.end(), [](const vector<int>& a, const vector<int>& b) {
            return a[1] < b[1];
        });

        int maxDay = 0;
        for (const auto& evt : events) {
            if (evt[1] > maxDay) {
                maxDay = evt[1];
            }
        }

        vector<int> nextDay(maxDay + 2);
        for (int d = 0; d < nextDay.size(); ++d) {
            nextDay[d] = d;
        }

        int count = 0;
        for (const auto& evt : events) {
            int start = evt[0];
            int end = evt[1];
            int day = findNext(nextDay, start);
            if (day <= end) {
                ++count;
                nextDay[day] = findNext(nextDay, day + 1);
            }
        }

        return count;
    }
};
