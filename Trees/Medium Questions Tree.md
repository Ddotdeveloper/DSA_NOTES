### Vertical Lvl
- thoda implementation vala hi question hai isme kuch aisa logic nhi hai khtarnak sa 
```cpp
class Solution {
public:
map<int,vector<pair<int,int> >> mp;
void solve(TreeNode* root, int x,int y){
	// base case
	if(root == NULL) return;
	mp[x].push_back({y,root->val});
	
	solve(root->left,x-1,y+1);
	solve(root->right,x+1,y+1);
	
	return;
}
	vector<vector<int>> verticalTraversal(TreeNode* root) {
	solve(root,0,0);
	vector<vector<int>> ans;
	
	for(auto i : mp){
	vector<pair<int,int>> tmp = i.second;
	// chote vala phle lena haii agar same levl pai 2 elements uske liye implementation 
	sort(tmp.begin(),tmp.end());
	vector<int> t;
	for(auto j : tmp) t.push_back(j.second);
	ans.push_back(t);
	}
	return ans;
	}
};
```

### Top and Bottem View Traversal 
- First Thing You have to use Queues for this I mean lvl order traversal's as it go lvl by lvl 
- The benift to go by level is given below 
  1. har level pai ham dekhenge ki left sai jayege and leftmost sai rightmost pai jayege bhdia sai 
   isme yeh hoga ki upar vale lvl ki priority jyadah hogi mast saii 
   Here is the picture of bfs 
   ![[Pasted image 20241008001606.png]]
  ab isme l tor r ja raha benificial haii 
```cpp
class Solution {
public:
    vector<int> topView(Node *root) {
        if (root == NULL) return {};  
        queue<pair<Node*, int>> q;
        map<int, int> topViewMap;
        q.push({root, 0});

        while (!q.empty()) {
            auto front = q.front();
            q.pop();
            Node* node = front.first;
            int hd = front.second;

            if (topViewMap.find(hd) == topViewMap.end()) {
                topViewMap[hd] = node->data; // top chaiye isliye isme yeh hua                  ki ek baar dalne ke bad dobbara nhi dalna 
            }

            if (node->left != NULL) {
                q.push({node->left, hd - 1});
            }

            if (node->right != NULL) {
                q.push({node->right, hd + 1});
            }
        }

        vector<int> ans;
        for (auto it : topViewMap) {
            ans.push_back(it.second);
        }

        return ans;
    }
};

```

#### Bottam View 
isme bss map vali chiz mai phle check nhi karna last vala dalna cause 
**Code:**
```cpp
class Solution {
public:
    vector<int> bottomView(Node *root) {
      if(root == NULL) return {};
      map<int,int> mp;
      queue<pair<Node*,int>> q;
      q.push({root,0});
      while(!q.empty()){
	      auto front = q.front();
		 q.pop();
	      Node* curr = front.first;
	      int x = front.second;
	      mp[x] = curr->val;
	      if(curr->left){
		      q.push({curr->left,x-1});
	      }
	      if(curr->right){
		      q.push({curr->right,x+1});
	      }
      }
      vector<int> ans;
      for(auto i : mp){
	      ans.push_back(i.second);
      }
	  return ans;
    }
};

```

  
 