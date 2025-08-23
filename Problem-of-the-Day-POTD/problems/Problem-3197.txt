class Solution {
public:
    // Function to calculate the minimum area of rectangle enclosing all ones in a submatrix 
    int minimumArea(vector<vector<int>>& grid, int st_i, int en_i, int st_j, int en_j) {
        int i, j, start_row = 1e9, end_row = -1, start_col = 1e9, end_col = -1, found = 0;
        for(i=st_i;i<=en_i;i++)    for(j=st_j;j<=en_j;j++){
            if(grid[i][j]){
                start_row = min(start_row, i);
                end_row = max(end_row, i);
                start_col = min(start_col, j);
                end_col = max(end_col, j);
                found = 1;
            }
        }
        return found ? ((end_row - start_row + 1) * (end_col - start_col + 1)) : 0;
    }
    
    int minimumSum(vector<vector<int>>& grid) {
        int i, j, m = grid.size(), n = grid[0].size(), ans = 1e9, one, two, three;

        /*
        -------------
        |    (1)    |
        |           |
        -------------
        | (2) | (3) |
        |     |     |
        -------------
        */
        for(i=0;i<m;i++){
            one = minimumArea(grid, 0, i, 0, n - 1);
            for(j=0;j<n;j++){
                two = minimumArea(grid, i + 1, m - 1, 0, j);
                three = minimumArea(grid, i + 1, m - 1, j+1, n-1);
                ans = min(ans, one + two + three);
            }
        }
        
        /*
        -------------
        |     | (2) |
        |     |     |
          (1) -------
        |     |     |
        |     | (3) |
        -------------
        */
        for(j=0;j<n;j++){
            one = minimumArea(grid, 0, m-1, 0, j);
            for(i=0;i<m;i++){
                two = minimumArea(grid, 0, i, j+1, n-1);
                three = minimumArea(grid, i + 1, m - 1, j+1, n-1);
                ans = min(ans, one + two + three);
            }
        }
        
        /*
        -------------
        |     |     |
        | (2) |     |
        ------- (1) |
        |     |     |
        | (3) |     |
        -------------
        */
        for(j=n-1;j>=0;j--){
            one = minimumArea(grid, 0, m-1, j+1, n-1);
            for(i=0;i<m;i++){
                two = minimumArea(grid, 0, i, 0, j);
                three = minimumArea(grid, i + 1, m - 1, 0, j);
                ans = min(ans, one + two + three);
            }
        }
                
                
        /*
        -------------
        | (2) | (3) |
        |     |     |
        ------------
        |           |
        |    (1)    |
        -------------
        */
        for(i=m-1;i>=0;i--){
            one = minimumArea(grid, i+1, m-1, 0, n - 1);
            for(j=0;j<n;j++){
                two = minimumArea(grid, 0, i, 0, j);
                three = minimumArea(grid, 0, i, j+1, n-1);
                ans = min(ans, one + two + three);
            }
        }
        
        /*
        -------------
        |    (1)    |
        -------------
        |    (2)    |
        -------------
        |    (3)    |
        -------------
        */
        for(i=0;i<m;i++){
            for(j=i+1;j<m;j++){
                one = minimumArea(grid, 0, i, 0, n-1);
                two = minimumArea(grid, i+1, j, 0, n-1);
                three = minimumArea(grid, j+1, m-1, 0, n-1);
                ans = min(ans, one + two + three);
            }
        }
        
         /*
        -------------
        |   |   |   |
        |   |   |   |
        |(1)|(2)|(3)|
        |   |   |   |
        |   |   |   |
        -------------
        */        
        for(i=0;i<n;i++){
            for(j=i+1;j<n;j++){
                one = minimumArea(grid, 0, m-1, 0, i);
                two = minimumArea(grid, 0, m-1, i+1, j);
                three = minimumArea(grid, 0, m-1, j+1, n-1);
                ans = min(ans, one + two + three);
            }
        }
        
        return ans;
    }
};
