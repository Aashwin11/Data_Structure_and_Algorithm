#include <vector>
#include <string>
#include <unordered_map>
#include <algorithm>

using namespace std;

struct Node {
    string name;
    unordered_map<string, Node*> children;
    string signature;

    Node(string name) : name(name) {}
};

class Solution {
public:
    vector<vector<string>> deleteDuplicateFolder(vector<vector<string>>& paths) {
        Node* root = new Node("");
        for (const auto& path : paths) {
            Node* curr = root;
            for (const string& folder : path) {
                if (curr->children.find(folder) == curr->children.end()) {
                    curr->children[folder] = new Node(folder);
                }
                curr = curr->children[folder];
            }
        }

        unordered_map<string, int> signatureCount;
        dfs(root, signatureCount);

        vector<vector<string>> result;
        vector<string> currentPath;
        for (const auto& [name, child] : root->children) {
            dfs2(child, currentPath, result, signatureCount);
        }

        delete root;
        return result;
    }

private:
    void dfs(Node* node, unordered_map<string, int>& signatureCount) {
        if (node->children.empty()) {
            node->signature = "";
            return;
        }

        vector<string> childSignatures;
        for (const auto& [name, child] : node->children) {
            dfs(child, signatureCount);
            childSignatures.push_back(name + "(" + child->signature + ")");
        }
        sort(childSignatures.begin(), childSignatures.end());
        node->signature = "";
        for (const string& sig : childSignatures) {
            node->signature += sig;
        }
        signatureCount[node->signature]++;
    }

    void dfs2(Node* node, vector<string>& currentPath, vector<vector<string>>& result, unordered_map<string, int>& signatureCount) {
        if (!node->children.empty() && signatureCount[node->signature] >= 2) {
            return;
        }
        currentPath.push_back(node->name);
        result.push_back(currentPath);
        for (const auto& [name, child] : node->children) {
            dfs2(child, currentPath, result, signatureCount);
        }
        currentPath.pop_back();
    }
};
