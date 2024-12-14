![](at/Pasted%20image%2020241214230030.png)
- it is the normal question for the but the tabulation Code will teach thing very important 
#### The Memoization Code 
```c++
// User function template for C++
class Solution {
  public:
    bool solve(int i, int t, vector<int> &arr,vector<vector<int>> &dp){
        // base case 
        int n = arr.size();
        
        if(t == 0) return true;
        if(i>=n) return false;
        if(dp[i][t] != -1 ) return dp[i][t];
        // case 
        bool pick = false;
        if(t-arr[i] >= 0) pick = solve(i+1,t-arr[i],arr,dp);
        bool not_pick = solve(i+1,t,arr,dp);
        
        return dp[i][t] = pick or not_pick;
        
    }
    bool isSubsetSum(vector<int>& arr, int target) {
        int n = arr.size();
        vector<vector<int>> dp(n+1,vector<int>(target+1,-1));
        return solve(0,target,arr,dp);
    }
};

```

##### Explanations 
- What the solve(i,target ) repersents
solve(ind,target ) = > is ind to n-1 index and if target is achievable or not give true or false at this state 
###### Base case Expalin 
if i>=n means no element are there so it will give false in every situation as nor target is achievable and also if t == 0 is achieved first then it will return true as it is 
solve(ind,0) return true // in any situation at any value of ind 

###### Rec Cases Expalin 
Explain the pick vala case why if and pick is false by default 
- neg isliye nhi jane diya cause fydah nhi haii kuch cause sare number postive haii ek baar target < 0 ho gya toh uspe koi chance nhi positive hone ka 
- bool is like kya pta true de de but by default toh false hi manna padega na usse true man lenge toh dikkat haii jiss case mai utha hi ni skte usse voh toh false hi dega na 
- agar true dega toh not pick vala case smbhal hi lega na tuje kya dikkat usse 

