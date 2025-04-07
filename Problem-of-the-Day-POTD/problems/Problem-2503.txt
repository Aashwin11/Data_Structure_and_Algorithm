class Solution {
public:
    vector<int> maxPoints(vector<vector<int>>& grid, vector<int>& queries) {
        int rowCount = grid.size(), colCount = grid[0].size();
        vector<int> result(queries.size(), 0);
        // Directions for movement (right, down, left, up)
        vector<pair<int, int>> DIRECTIONS = {{0, 1}, {1, 0}, {0, -1}, {-1, 0}};

        // Store queries along with their original indices to restore order
        // later
        vector<pair<int, int>> sortedQueries;
        for (int index = 0; index < queries.size(); index++) {
            sortedQueries.push_back({queries[index], index});
        }
        // Sort queries by value in ascending order
        sort(sortedQueries.begin(), sortedQueries.end());

        // Min-heap (priority queue) to process cells in increasing order of
        // value
        priority_queue<pair<int, pair<int, int>>,
                       vector<pair<int, pair<int, int>>>, greater<>>
            minHeap;
        vector<vector<bool>> visited(rowCount, vector<bool>(colCount, false));
        // Keeps track of the number of cells processed
        int totalPoints = 0;
        // Start from the top-left cell
        minHeap.push({grid[0][0], {0, 0}});
        visited[0][0] = true;

        // Process queries in sorted order
        for (auto [queryValue, queryIndex] : sortedQueries) {
            // Expand the cells that are smaller than the current query value
            while (!minHeap.empty() && minHeap.top().first < queryValue) {
                auto [cellValue, position] = minHeap.top();
                minHeap.pop();
                int currentRow = position.first, currentCol = position.second;
                // Increment count of valid cells
                totalPoints++;

                // Explore all four possible directions
                for (auto [rowOffset, colOffset] : DIRECTIONS) {
                    int newRow = currentRow + rowOffset,
                        newCol = currentCol + colOffset;

                    // Check if the new cell is within bounds and not visited
                    if (newRow >= 0 && newCol >= 0 && newRow < rowCount &&
                        newCol < colCount && !visited[newRow][newCol]) {
                        minHeap.push({grid[newRow][newCol], {newRow, newCol}});
                        // Mark as visited
                        visited[newRow][newCol] = true;
                    }
                }
            }
            // Store the result for this query
            result[queryIndex] = totalPoints;
        }
        return result;
    }
};
