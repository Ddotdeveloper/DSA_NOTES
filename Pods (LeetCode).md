## Maximal Score After Applying K Operations
[2530. Maximal Score After Applying K Operations](https://leetcode.com/problems/maximal-score-after-applying-k-operations/)
Observation 
1. Sorting Will not affect anything 
2. We need Greatest after every operation Sounds Like a (Max_heap) 
```cpp
class Solution {

public:

typedef long long ll;

long long maxKelements(vector<int>& nums, int k) {

ll ans = 0;

priority_queue<ll> pq;

for(auto i : nums) pq.push((ll)i);

	while(k>0){
	auto top = pq.top();
	pq.pop();
	ans += top;
	double new_top = (double)top/3.0;
	new_top = ceil(new_top);
	pq.push((ll)new_top);
	k--;
  }
	return ans;
	}
};
```
### Key Points 
1. dobule typecast vali chiz and double can store the decimal values 
2. ceil func
## Smallest Range Covering Element From K list 
### Observations 
1. Given k lists 
2. smallest Range 
   We define the range `[a, b]` is smaller than range `[c, d]` if `b - a < d - c` **or** `a < c` if `b - a == d - c`.
   - at the left side we have to increase it's values 
   - at the right side we have to decrease it's value 
### Approach 
1. Store all elements in the array and sort it 
2. check for the left value by traversing this array and find the greatest which is poosible 

  