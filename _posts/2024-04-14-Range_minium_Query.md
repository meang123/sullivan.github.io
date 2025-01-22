---
layout: single
title:  "Range Minimum Query"
categories: RMQ,sparse table,segement tree
tag : [algorithm,RMQ,Range Minimum Query,sparse table,segement tree]
toc: true
author_profile: false
sidebar:
  nav : "docs"
search: true
typora-root-url: ../
---





# Range Minimum Query 



**해결 하려는 문제** : 배열이 있을때 다양한 범위를 가진 Query가 왔을때 최소 값을 반환하는 문제를 해결하려고 한다 



### Solution 



**Brute force** : 배열의 요소를 모두 보고 나서 최소 값 반환 하는 방법 O(N)



**query lookup table** : query look up table을 만들어서 모든 범위에 대해서 최소값을 table에 저장하는 방법 
$$
Time complex : O(N^2) \\

Query time : O(1)
$$


**square root decomposition**



배열 길이 n을 sqrt n으로 나누어서 생각하는 방식이다 sqrt n만큼 나누어진 부분에서 최소값을 찾는다 

<img src="https://blog.kakaocdn.net/dn/dPREh8/btrhVs7hzua/BkkqopK09h7ZAQLswtH9lK/img.jpg" alt="img" style="zoom:30%;" />



위에 사진 처럼 query의 범위 길이 n에서 sqrt n만큼 나누어서 최소값 구하고 최종으로 최소값을 고르는 형식이다 예제처럼 Q(4,7)에서 업데이트가 되어서 Q(2,7)이 되어도 sqrt n만큼 관찰하므로 O(sqrt n) 을 만족 한다 









**Segment Tree** [업데이트 해야함]

https://www.youtube.com/watch?v=2FShdqn-Oz8



**sparse Table**



<img src="https://blog.kakaocdn.net/dn/bijBdc/btrhTcxqZ3E/M1iuAH5DadVPkKhkMp9lcK/img.jpg" alt="img" style="zoom:33%;" />



위에 그림 처럼 2의 n승 단위로 묶어서 미리 최솟값을 구한다 



<img src="https://blog.kakaocdn.net/dn/5r9G5/btrhVrUQ2WJ/VKhVObMC9k8UoECn3OO6k0/img.jpg" alt="img" style="zoom:33%;" />

그러면 전처리에서 구한 최소값을  이용해서 구할수있는데 이때 overlap 되어있는 부분 포함해도 쿼리당 O(1)으로 처리 할수있다 하지만 업데이트는 불가능 하다 

Q(L,R)을 처리 하기 위해 length = R-L +1의 2의 power가 몇인지 구해야 한다 log로 계산 할수가 있다 그 값이 j라고 할때 min(min[L] [j]),min([R-(1<<j)+1] [j]) 가 되어야 overlap도 포함할수가 있다 

L시작에서 j만큼의 범위 잡는것과 , R의 시작점을 잡아야 하는데 R의 범위를 넘으면 안되니까 R-1<<j  +1로 시작점을 잡고 j개의 범위를 잡는것이다 

 

```c++

//RMQ sparse table

#include <iostream>
using namespace std;

const int MAX_N = 500;
cont int LOG = 17;
int lookup[MAX_N][LOG]; //2^17
int query(int L,int R)
{
    int length = R-L + 1;
    int k=0;
    while((1<<(k+1))<=length)
    {
        k++;
    }
    
    
    return min(lookup[L][k],lookup[R-(1<<k)+1][k]);
    
}

int main()
{
    int n =0;
    cin>>n;
    for(int i =0;i<n;i++)
    {
        cin>>lookup[i][0];
    }
    //preprocess
    //2,4,8,16....untill 2^17
    /*
    배열의 요소가 l[i][0]에 들어가 있고 2,4,8,16..에 대해서는 
    l[i][1], l[i][2]....에 저장됨 4는 2에서 계산한것 가지고 계산 
    8은 4에서 계산한 것 가지고 계산 이런식으로 진행됨 
    
    */
    for(int j=1;j<LOG;j++)
    {
        for(int i=0;i+(1<<j)-1<n;i++)
        {
            //1<<(j-1)이 부분은 2의 j-1승을 의미한다 Q(4,7)일때 4번째 요소에서 2의 승 만큼 이동한 부분에서 
            //출발 지점 잡기 위해서이다
            lookup[i][j] = min(lookup[i][j-1],lookup[i+(1<<(j-1)][j-1]);
        }
    }
    //answer query 
    int q=0;
    cin>>q;
    for(int i =0;i<q;i++)
    {
        int L=0,R=0; //Q(L,R)
        cin>>L>>R;
    	cout<<query(L,R)<<endl;
    }
    
    
    return 0;
}


```



**LCA(lowest common ancestor)** 로 해결 



LCA : 임의의 두 노드를 모두 포함하는 서브 트리중 가장 작은 것을 찾는 문제이다 (Tree 파트에서 LCA정리 내용 있다 )



**RMQ -> LCA** : stack을 이요해서 **cartesian tree**를 O(n)으로 구현 하고 LCA로 문제를 풀면 RMQ를 해결할수가 있다 (Tree 파트에서 caresian tree정리 내용 있다 )



**LCA -> RMQ** : DFS를 이용해서 (depth,element)로 만들고 난이후 그리고 나서 RMQ로 문제를 풀면 LCA문제 해결 할수있다 





---------





## 참고 사이트 



https://stementor.tistory.com/entry/Range-Minimum-Query%EB%A5%BC-%ED%86%B5%ED%95%B4-%EC%82%B4%ED%8E%B4%EB%B3%B4%EB%8A%94-%EC%BB%B4%ED%93%A8%ED%84%B0-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98



[Range Minimum Query (Square Root Decomposition and Sparse Table) - GeeksforGeeks](https://www.geeksforgeeks.org/range-minimum-query-for-static-array/)









 