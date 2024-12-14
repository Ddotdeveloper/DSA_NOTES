#### BFS and DFS Teqns
[200. Number of Islands](https://leetcode.com/problems/number-of-islands/)
```cpp
class Solution {
public:
    vector<int> dirx = {0, 1, 0, -1};
    vector<int> diry = {1, 0, -1, 0};
    void bfs(int i, int j, vector<vector<int>>& vis,
             vector<vector<char>>& grid) {
        int n = grid.size();
        int m = grid[0].size();
        queue<pair<int, int>> q;
        q.push({i, j});
        while (!q.empty()) {
            auto f = q.front();
            q.pop();
            int ci = f.first;
            int cj = f.second;
            for (int k = 0; k < 4; k++) {
                int di = ci + dirx[k];
                int dj = cj + diry[k];
                if (di < n and di >= 0 and dj < m and dj >= 0 and
                    vis[di][dj] == 0 and grid[di][dj] == '1') {
                    vis[di][dj] = 1;
                    q.push({di, dj});
                }
            }
        }
    }
    int numIslands(vector<vector<char>>& grid) {
        int n = grid.size();
        int m = grid[0].size();
        vector<vector<int>> vis(n, vector<int>(m, 0));
        int count = 0;
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                if (vis[i][j] == 0 and grid[i][j] == '1') {
                    vis[i][j] = 1;
                    bfs(i, j, vis, grid);
                    count++;
                }
            }
        }

        return count;
    }
};
```

- This can be done by the dsu also 
- just normal traversal and code for disconnected componets check karne vala code Use kar lo bdhia saii 
#### Check cycle in the Undiretected graph
- if you find some node already visited other than the parent node then there is the cycle 
- Same kind of traversal implementation in both the bfs and dfs just have to traverse the graph and check for the above condition 

#### Topo sort by Bfs in Directed  and Cycle detection directed (Khan's Algo)

```cpp
class Solution {
public:
    bool bfs(int node, vector<int>& inDeg, unordered_map<int, vector<int>>& adj,
             int n) {
        queue<int> q;
        int siz = 0;
        for (int i = 0; i < n; i++) {
            if (inDeg[i] == 0)
                q.push(i);
        }

        while (!q.empty()) {
            int curr_node = q.front();
            q.pop();
            siz++;
            for (auto child : adj[curr_node]) {
                inDeg[child]--;
                if (inDeg[child] == 0) {
                    q.push(child);
                }
            }
        }

        return siz == n;
    }

    bool canFinish(int n, vector<vector<int>>& prerequisites) {
        unordered_map<int, vector<int>> adj;
        vector<int> inDeg(n, 0);
        for (auto p : prerequisites) {
            int a = p[0];
            int b = p[1];
            adj[b].push_back(a); // Changed the direction to b -> a as per
                                 // course dependency logic
            inDeg[a]++;
        }

        return bfs(0, inDeg, adj, n);
    }
};
```
- Use of khan's algo for the detection of the cycle in graph
- Isme yeh chiz ki galti bar bar kar deta ki auto vala loop mai lagaya kar inDeg maii 
- Similar Algo can be used to find the top sort in graph 
#### Check Cycle by Dfs in directed 
- Main key takeaway is the `path_vis` array 
- `path_vis` it tell which node are visted in the current path okkay 
- There is cycle if we find a node which is visited and also in the same path that means there is cycle 

```cpp
class Solution {
public:
    bool dfs(int node, vector<int> &vis, vector<int> &path_vis, unordered_map<int,vector<int>> &adj){
    
        vis[node] = 1;
        path_vis[node] = 1;
        for(auto child : adj[node]){
            if(vis[child] == 0){
                if(dfs(child, vis, path_vis, adj) == false) return false;
            }else if(path_vis[child] == 1){
                return false;
            }
        }

        path_vis[node] = 0;
        return true;
    }

    bool canFinish(int numCourses, vector<vector<int>>& prerequisites) {
        unordered_map<int,vector<int>> adj;
        for(auto p : prerequisites){
            int a = p[0];
            int b = p[1];
            adj[b].push_back(a);  // Changed the direction to b -> a as per course dependency logic
        }

        vector<int> vis(numCourses, 0);
        vector<int> path_vis(numCourses, 0);

        for(int i = 0; i < numCourses; i++){
            if(vis[i] == 0){
                if(dfs(i, vis, path_vis, adj) == false) return false;
            }
        }

        return true;
    }
};
```
#### Topo Sort by Dfs 
```cpp
class Solution
{
	public:
	//Function to return list containing vertices in Topological order. 
	void dfs(int node, vector<int> adj[], vector<int> &vis, stack<int> &s){
	    vis[node] = 1;
	    for(auto child : adj[node]){
	        if(vis[child] == 0){
	            vis[child] = 1;
	            dfs(child,adj,vis,s);
	        }
	    }
	    
	    s.push(node); // This is imp phle uske sare visit kar aayou fir dalo stack maii 
	    
	    return;
	}
	vector<int> topoSort(int V, vector<int> adj[]) 
	{
	    stack<int> s;
	    vector<int> vis(V,0);
	    for(int i = 0; i<V; i++){
	        if(vis[i] == 0){
	            vis[i] = 1;
	            dfs(i,adj,vis,s);
	        }
	    }
	    vector<int> ans;
	    while(!s.empty()){
	        int t = s.top();
	        ans.push_back(t);
	        s.pop();
	    }
	    
	   // for(auto i : ans) cout<<i<<" ";
	    
	    return ans;
	}
};
```
- Phle sare use niche ke sare vis kar aayu and vapis aate time stack mai dalo bhaii 
#### isGraph Bipartite ?
- Graph Bipartite means we can divide the nodes in grp of a and b with edges each node in a and b can be made in various ways this questions
- odd even cycle length can also be figure out by this method 
##### by Bfs 
```cpp
class Solution {
public:
    bool bfs(int node, vector<vector<int>> &adj, vector<int> &vis){
        queue<int> q;
        vis[node] = 0;
        q.push(node);
        while(!q.empty()){
            auto curr_node = q.front();
            q.pop();
            for(auto child : adj[curr_node]){
                if(vis[child] == -1){
                    if(vis[curr_node] == 0){
                        vis[child] = 1;
                    }else{
                        vis[child] = 0;
                    }
                        q.push(child);
                }
                else if(vis[child] == vis[curr_node]){
                    return false;
                }
            }
        }

        return true;

    }
    bool isBipartite(vector<vector<int>>& graph) {
        int n = graph.size();
        vector<int> vis(n,-1);
        for(int i = 0; i<graph.size(); i++){
            if(vis[i] == -1){
               if(!bfs(i,graph,vis)) return false;
            }
        }

        return true;
    }
};

```
##### By dfs 
- similar method almost but vahi chiz hame dfs karni padegi bhdia saiii
