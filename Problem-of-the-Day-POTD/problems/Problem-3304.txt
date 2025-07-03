class Solution {
public:
    static char kthCharacter(int k) {
        if (k==1) return 'a';
        int shift=0;
        for(int b=bit_ceil((unsigned)k); b>1; b>>=1) {
            if (k>b/2){
                k-=b/2;
                shift++;
            }
        }
        // 'a' shifted by how many times it moved into second half
        return 'a'+(shift%26);
    }
};
