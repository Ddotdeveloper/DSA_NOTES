This algo is used for finding the shortest distance where there is some edges negtive and also able to #detectnegitivecycle it can also detect the negitive cycle bhdia saii ek dum 
 ![[Pasted image 20240818190142.png]]
 Imp code snippit 
 1. we process the edges v-1 times v is here number of vertices 
 2. and at last also we again process it if the dis is reduced further that means there is a neg cycle 
 To process we do 
 ```cpp
          if(dis[u] != 1e8 and dis[u] + w < dis[v]){
                   dis[v] = dis[u] + w;
               }
    // the dis also should not be equal to the infite cause tabhi toh plus kar payege and 
    // intially dis[0] = 0; or in place of 0 source can be there 
```
