This is the linear ordering of the nodes in the dag very important in any kind of ordering question it can be used like in the pod you have seen about the matrix 
This problem is using the teq that is used finding the toposort by the dfs let me solve this  
### Find Eventual safe states
https://leetcode.com/problems/find-eventual-safe-states/

![[Pasted image 20240724002649.png]]
Yeh vala code mast haii isme jo bhi cycle ka part hote haii voh vale inRec array mai true rahte haii thik haii mast chiz ek dum let isse ham eventual safe state vala questio bhdia sai solve kar skte 

![[Pasted image 20240724002813.png]]
in rec vali array mai 0 1 and 3 are true isliye bhdia hai yeh jo bhi true hoga 
jo bhi true haii voh sare unsafe haii casue voh terminal state pai nhi ja rahe haii isilye bhdia 
isse apan direclty pta kar skte 
-> kyuki tum khud dekho jab bhi voh true hai usse bina false kiye maii na usse reeturn kar de raha hu so hamesha true rahega isliye thik haii 

