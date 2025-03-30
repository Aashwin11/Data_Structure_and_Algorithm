class Solution {
public:
    vector<int> partitionLabels(string s) {
        // Stores the last index of each character in 's'
        vector<int> lastOccurrence(26, 0);
        for (int i = 0; i < s.size(); ++i) {
            lastOccurrence[s[i] - 'a'] = i;
        }

        int partitionEnd = 0, partitionStart = 0;
        vector<int> partitionSizes;
        for (int i = 0; i < s.size(); ++i) {
            partitionEnd = max(partitionEnd, lastOccurrence[s[i] - 'a']);
            // End of the current partition
            if (i == partitionEnd) {
                partitionSizes.push_back(i - partitionStart + 1);
                partitionStart = i + 1;
            }
        }
        return partitionSizes;
    }
};
