class Solution {
public:
    static bool isPowerOfThree(int n) {
        int e=log(INT_MAX)/log(3);
        int N=pow(3, e);
        return n>0 && N%n==0;
    }
};
