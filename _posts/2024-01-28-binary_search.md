---
layout: single
title:  "binary search"
categories: search
tag: [c++,python,Algorithm,binary search,search,upper bound, lower bound]
toc: true
author_profile: false
sidebar:
  nav : "docs"
search: true
---



## binary search 

 정렬 된 상황에서 log n으로 탐색 할수있다 



```c++
# include <iostream>
using namespace std;
int binary_search(vector<int>&arr,int target)
{
    int left = 0;
    int right = arr.size()-1;
    int mid =0;
    while(left<=right)
    {
        mid = (left+right)/2;
        if(arr[mid]==target)
        {
            return mid;
        }
        if(arr[mid]>target)
        {
            right = mid-1;
        }
        else
        {
            left = mid+1;
        }
    }
    return -1;
}
int main()
{
    return 0;
}
```





----



# Upper bound / lower bound 



array 파트나 다른 파트에서 코드 예제 사용한게 있으니 참고 하면 될것 같다. 여기서는 간단한 개념 상기 정도만 언급 하고 넘어가겠다 



가정 : 이진 탐색 처럼 정렬이 되어있을때 사용할수있다 



**Lower bound**: 여러개의 같은 target val있을시 target <span style="background-color:#fff5b1">이상</span>의 값이 최초로 나오는 위치 (target val 첫 위치 반환)



**upper bound** : 여러개의 같은 target val있을시 target <span style="background-color:#fff5b1">초과</span>의값이 최초로 나오는 위치(target val 마지막 초과 위치 반환)



1. upper - lower 은 배열 내에 traget val의 개수를 알수있다 즉 존재하는 구간 알수있다
2. upper와 lower의 위치가 같다면 배열내에 target val이 없다고 할수있다 





 
