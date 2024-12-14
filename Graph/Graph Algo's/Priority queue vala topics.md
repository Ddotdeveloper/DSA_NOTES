### Cheap Flights vala Imp question &&
https://leetcode.com/problems/cheapest-flights-within-k-stops/description/
![[Pasted image 20240818181900.png]]
![[Pasted image 20240818182426.png]]
Important Points for this are here 
-  Ki isme jo hai pq use nhi hoga only queue use hoga
it is because in this steps jydah imp hai naki distance and minmum distance yaha nikalne mai hamri help karega min distance array but hame phle steps ko consider karna naki dis min ko and steps ko consider karn ke liye toh normal bfs hi bhaut hai smje 
-> isme yah toh pq lagao toh stops pai lagao dis pai nhi and stops pai lagane ka benifit nhi haii cause voh toh direct bfs haii simple sa 

## Number of ways vala concept to dst throgh the shortest distance 
https://leetcode.com/problems/number-of-ways-to-arrive-at-destination/description/
![[Pasted image 20240818182922.png]]
![[Pasted image 20240818182936.png]]
```
class Solution {

public:

int mod = 1e9 + 7;

typedef pair<long long, int> P; // Ensure the distance in the pair is long long

  

int countPaths(int n, vector<vector<int>>& roads) {

unordered_map<int, vector<vector<int>>> adj;

for (auto edge : roads) {

int a = edge[0];

int b = edge[1];

int w = edge[2];

adj[a].push_back({b, w});

adj[b].push_back({a, w});

}

  

vector<long long> dis(n, LLONG_MAX); // Use LLONG_MAX for long long initialization

vector<long long> ways(n, 0); // this is an array ways array 

priority_queue<P, vector<P>, greater<P>> pq;

pq.push({0, 0}); // dis, node

dis[0] = 0;

ways[0] = 1;

  

while (!pq.empty()) {

long long d = pq.top().first;

int node = pq.top().second;

pq.pop();

  

if (d > dis[node]) continue; // Skip if this is not the shortest path anymore

  

for (auto child : adj[node]) {

int child_node = child[0];

long long child_dis = child[1];

  

if (d + child_dis < dis[child_node]) {

dis[child_node] = d + child_dis;

ways[child_node] = ways[node];

// and if you find a shorter path through node you will do make ways of child node == ways of prarent(node)

pq.push({dis[child_node], child_node});

} else if (d + child_dis == dis[child_node]) {

ways[child_node] = (ways[node] + ways[child_node]) % mod; // when you find the dis which is equal to the smaller path 

}

}

}

  

return ways[n - 1] % mod;

}

};

```
### Important Points 
1. formation and updation of the ways array for keeping the track of the ways till the node 
the significane of this arrays is that it tell the ways of shortest path from the source node to that particular node 
2. the two important thing how to upadate this see the code /
-  to update that it is 2 ways in which you get a new shortest path or got the path == shortest path in both siuations you can check in the code above 
