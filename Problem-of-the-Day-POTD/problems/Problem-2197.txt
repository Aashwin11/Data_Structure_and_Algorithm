class Solution {
public:
    vector<int> replaceNonCoprimes(vector<int>& nums) {
        vector<int> stack;
        for (int num : nums) {
            while (!stack.empty()) {
                int top = stack.back();
                int g = gcd(top, num);
                if (g == 1) {
                    break;
                }
                stack.pop_back();
                // compute LCM
                long long merged = (long long)top / g * num;
                num = (int)merged;
            }
            stack.push_back(num);
        }
        return stack;
    }
    
private:
    int gcd(int a, int b) {
        return b == 0 ? a : gcd(b, a % b);
    }
};
