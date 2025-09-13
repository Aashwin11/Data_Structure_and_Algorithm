class Solution {
public:
    int maxFreqSum(std::string s) {
        std::unordered_map<char, int> freq;
        int con = 0, vow = 0;
        for (char c : s) freq[c]++;
        for (auto& [ch, count] : freq) {
            if (std::string("aeiou").find(ch) != std::string::npos)
                vow = std::max(vow, count);
            else
                con = std::max(con, count);
        }
        return con + vow;
    }
};
