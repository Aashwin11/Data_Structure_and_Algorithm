/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    int i=0;
    TreeNode* recoverFromPreorder(string& T, int depth=0) {
        if (i>=T.size()) return NULL; //base case
        int D=0;
        
        while (T[i]=='-') D++, i++; //D dashes
        
        // If the current depth is less than expected, reset i
        if (D < depth) {
            i-=D;  // Reset i
            return NULL;
        }
        
        // Read the node value
        int x=0;
        while (isdigit(T[i])) {
            x=x*10+T[i]-'0';
            i++;
        }
        
        // Create node
        TreeNode* node=new TreeNode(x);
        
        // recover left and right children
        node->left=recoverFromPreorder(T, depth+1);
        node->right=recoverFromPreorder(T, depth+1);
        
        return node;
    }
};
