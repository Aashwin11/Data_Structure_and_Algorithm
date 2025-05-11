class Solution {
public:
    bool threeConsecutiveOdds(vector<int>& arr) {
        int odds = 0;
        for (int i = 0 ; i < arr.size() ; i++) {
            if (arr[i] & 1) ++odds;
            else odds = 0;
            if (odds == 3) return true;
        }
        return false;
    }
};
