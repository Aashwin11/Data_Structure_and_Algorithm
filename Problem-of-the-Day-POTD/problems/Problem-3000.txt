class Solution {
public:
    int areaOfMaxDiagonal(vector<vector<int>>& dimensions) {
        int maxArea=0, Mdia2=0;
        for (auto& r: dimensions){
            int w=r[0], h=r[1], dia2=w*w+h*h;
            if (Mdia2<dia2){
                Mdia2=dia2;
                maxArea=0;
            }
            if (dia2==Mdia2)
                maxArea=max(maxArea, w*h);
        }
        return maxArea;
    }
};
