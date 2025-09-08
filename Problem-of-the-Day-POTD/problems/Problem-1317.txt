class Solution {
public:
    vector<int> getNoZeroIntegers(int n) {
        int a=0, b= 0, tens=1;
        for (; n>0; n/=10, tens*=10) {
            int d=n%10;
            if (d==0) {
                // borrow from next higher digit: 5+5
                a+=5*tens;
                b+=5*tens;
                n-=10;  // subtract from the next digit
            } 
            else if (d==1 && n>=10) {
                a+=6*tens;
                b+=5*tens;
                n-=10;  // borrow
            } 
            else {
                // normal split
                a+=(d-d/2)*tens;
                b+=(d/2)*tens;
            }
        }
        return {a, b};
    }
};


