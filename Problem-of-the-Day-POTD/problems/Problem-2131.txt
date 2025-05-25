class Solution {
public:
    int longestPalindrome(vector<string>& words) {
        unordered_map<string, int> mpp;
        for (string w : words) mpp[w]++;

        int count = 0, alreadyPalindrome = 0;
        for (auto& [w, freq] : mpp) {
            string s = w;
            reverse(s.begin(), s.end());
            if (w == s) {
                count += (freq / 2) * 4;
                if (freq % 2) alreadyPalindrome = 1;
            } else if (w < s && mpp.count(s)) {
                count += min(freq, mpp[s]) * 4;
            }
        }
        return count + alreadyPalindrome * 2;
    }
};
