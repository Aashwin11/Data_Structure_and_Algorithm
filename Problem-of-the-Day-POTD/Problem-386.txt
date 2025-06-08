class Compare 
{
public:
    bool operator()(int a, int b) 
    {
        // Step 1: Custom comparator
        return to_string(a) > to_string(b); 
    }
};

class Solution 
{
public:
    vector<int> lexicalOrder(int n) 
    {
        // Step 1: Create priority queue with custom comparator
        priority_queue<int, vector<int>, Compare> pq;

        // Step 2: Insert numbers 1 to n into the heap
        for (int i = 1; i <= n; ++i) 
        {
            pq.push(i);
        }

        // Step 3: Prepare result vector
        vector<int> result;

        // Step 4: Extract elements in lexicographic order
        while (!pq.empty()) 
        {
            result.push_back(pq.top());
            pq.pop();
        }

        // Step 5: Return the result
        return result;
    }
};
