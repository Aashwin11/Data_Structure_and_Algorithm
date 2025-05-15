class Solution {
public:
    vector<string> getLongestSubsequence(vector<string>& words, vector<int>& groups) {
        vector<string> result;
        int last = -1;
        for (int i = 0; i < words.size(); ++i) {
            if (groups[i] != last) {
                result.push_back(words[i]);
                last = groups[i];
            }
        }
        return result;
    }
};
