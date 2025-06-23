### Level Order Traversal 
Level Order Traversal (also known as Breadth-First Traversal) of a binary tree means visiting the nodes level by level from top to bottom and left to right within each level.

✅ Example:
Given a binary tree:
```
      1
     / \
    2   3
   / \   \
  4   5   6
```
  
Level Order Traversal Output:
[ [1], [2, 3], [4, 5, 6] ]

```
#include <iostream>
#include <vector>
#include <queue>
using namespace std;

struct TreeNode {
    int val;
    TreeNode *left, *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};

vector<vector<int>> levelOrder(TreeNode* root) {
    vector<vector<int>> result;
    if (!root) return result;

    queue<TreeNode*> q;
    q.push(root);

    while (!q.empty()) {
        int levelSize = q.size();
        vector<int> currentLevel;

        for (int i = 0; i < levelSize; ++i) {
            TreeNode* curr = q.front(); q.pop();
            currentLevel.push_back(curr->val);
            if (curr->left) q.push(curr->left);
            if (curr->right) q.push(curr->right);
        }
        result.push_back(currentLevel);
    }
    return result;
}

```
## Depth First Traversal

### In-Order Traversal
In-order (Left → Node → Right)

```
void inorderIterative(TreeNode* root) {
    stack<TreeNode*> st;
    TreeNode* curr = root;

    while (curr != nullptr || !st.empty()) {
        while (curr != nullptr) {
            st.push(curr);
            curr = curr->left;
        }
        curr = st.top(); st.pop();
        cout << curr->val << " ";
        curr = curr->right;
    }
}

```

### Pre-order Traversal (Iterative)
Visit order: Node → Left → Right

```
void preorderIterative(TreeNode* root) {
    if (!root) return;

    stack<TreeNode*> st;
    st.push(root);

    while (!st.empty()) {
        TreeNode* node = st.top();
        st.pop();
        cout << node->val << " ";

        // Push right first so left is processed first
        if (node->right) st.push(node->right);
        if (node->left)  st.push(node->left);
    }
}
```


### Post-order Traversal (Iterative using two stacks)
Visit order: Left → Right → Node

```
void postorderIterative(TreeNode* root) {
    if (!root) return;

    stack<TreeNode*> st1, st2;
    st1.push(root);

    while (!st1.empty()) {
        TreeNode* node = st1.top(); st1.pop();
        st2.push(node);

        if (node->left)  st1.push(node->left);
        if (node->right) st1.push(node->right);
    }

    while (!st2.empty()) {
        cout << st2.top()->val << " ";
        st2.pop();
    }
}
```
### In-Order, Pre-Order and Post-order through recursion

🔍 When to Use Recursion  
✅ Use recursion when:  
1. Tree size is moderate (≤10,000 nodes)  
2. You need quick and clear code  
3. You're doing DFS-like traversals (in-order, pre-order, post-order)  

🔍 When to Use Iteration (Loop)  
✅ Use iteration with stack when:    
1. Tree is very deep (e.g., >100,000 levels) — recursion may crash  
2. You need explicit control over the traversal steps  
3. You're building non-recursive libraries, frameworks, or embedded systems  

```
#include <iostream>
using namespace std;

// Define a basic TreeNode
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};

// In-order Traversal: Left → Node → Right
void inorder(TreeNode* root) {
    if (!root) return;
    inorder(root->left);
    cout << root->val << " ";
    inorder(root->right);
}

// Pre-order Traversal: Node → Left → Right
void preorder(TreeNode* root) {
    if (!root) return;
    cout << root->val << " ";
    preorder(root->left);
    preorder(root->right);
}

// Post-order Traversal: Left → Right → Node
void postorder(TreeNode* root) {
    if (!root) return;
    postorder(root->left);
    postorder(root->right);
    cout << root->val << " ";
}

int main() {
    /*
        Example Tree:
        
              50
             /  \
           30    70
          / \     \
        80  10     5
    */
    
    TreeNode* root = new TreeNode(50);
    root->left = new TreeNode(30);
    root->right = new TreeNode(70);
    root->left->left = new TreeNode(80);
    root->left->right = new TreeNode(10);
    root->right->right = new TreeNode(5);

    cout << "In-order Traversal: ";
    inorder(root);
    cout << "\n";

    cout << "Pre-order Traversal: ";
    preorder(root);
    cout << "\n";

    cout << "Post-order Traversal: ";
    postorder(root);
    cout << "\n";

    return 0;
}

```
