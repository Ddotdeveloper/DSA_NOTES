### Lowest Commen Anchestores 
![[Pasted image 20241007174142.png]]
#### Here are some key Points 
- TreeNode is Returning can be a null or TreeNode or both null 
- if(one of them is null other is not then you return the non null vala node ) like at 5 it return (7) as left gives here null and right gives the 7 so it return 7 
- Our lcs is where both sides return not null values that is our lcs and at 2 we return 2 as it is our lcs 
```cpp
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        //base case
        if (root == NULL || root == p || root == q) {
            return root;
        }
        TreeNode* left = lowestCommonAncestor(root->left, p, q);
        TreeNode* right = lowestCommonAncestor(root->right, p, q);

        //result
        if(left == NULL) {
            return right; // if one is non null return right
        }
        else if(right == NULL) {
            return left; // if right is null we rturn the left 
        }
        else { //both left and right are not null, we found our result
            return root;
        }
    }
};
```

### Left View 
### This Wrong Code 
```cpp
void solve(Node* root, vector<int> &ans){
    if(root == NULL) return;
    
    ans.push_back(root->data);
    
    if(root->left != NULL){
        solve(root->left,ans);
    }else{
            solve(root->right,ans);
    }
    return;
}
vector<int> leftView(Node *root)
{
    vector<int> ans;
    solve(root,ans);
    return ans;
}
```
#### Why Wrong 
as it is not covering all the lvls it left some of lvls 

### Sahi vala Code
#### Real Def of Left View 
- When we write the normal way of traversal like left and then right 
- Then first node appear at each level is the Left view of that level 
- That's why we make a vis lvl and then mark only if `vis(lvl)` when there is not -1

```cpp
void solve(Node* root,int lvl, vector<int> &vis){
    // base case
    if(root == NULL) return;
    if(vis[lvl] == -1) vis[lvl] = root->data; // if lvl is visited than do not mark it mark the only level which is showing -1 
    solve(root->left,lvl+1,vis);
    solve(root->right,lvl+1,vis);
    
    return;
}
vector<int> leftView(Node *root)
{
    vector<int> vis(1000,-1);
    solve(root,0,vis);
    vector<int> ans;
    for(auto i : vis) 
    // Now pushing of the i in the ans vector 
    if(i != -1) ans.push_back(i);
    else break;
    
   return ans;
}
```

