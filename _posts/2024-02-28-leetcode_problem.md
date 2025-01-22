---
layout: single
title:  "leetcode problem collection"
categories: algorithm,leetcode, collection
tag : [algorithm,leetcode,C++,python,c++]
toc: true
author_profile: false
sidebar:
  nav : "docs"
search: true
typora-root-url: ../


---





# leet code 문제 모음집 



leetcode에서 풀었던 여러가지 문제들의 모임집 해결 하는 과정을 담고 실제 해결한 방식 + 다른 사람이 해결한 방법과 비교하여 정리 한다 



-----



### Single Number 

중복하지 않는 숫자를 배열에서 찾는 간단한 문제였다.  단 O(N)의 시간 복잡도와 O(1)의 추가 공간을 사용해야 하는 제한이 있었다. 배열 요소의 범위는 -30000~30000까지 였다.   처음에 set이 생각 났지만 다른 방식을 생각 해 보았을때 간단하게는 find나 count를 사용하면 어떨까 했지만 N의 시간복잡도에서 해결해야 하기 때문에 적절하지 않았다. 그래서 -1을 곱하면서 중복 확인하면 좋지 않을까? 했는데 양수였으면 괜찮았는데 음수여서 해결이 안될것 같았다. 그래서 결국 set을 사용해서 중복 확인을 하였고 set에 남아있는 요소를 반환하는 방식으로 해결 하였다 다음은 set으로 해결한 코드이다 



```c++
class Solution {
public:
    int singleNumber(vector<int>& nums) 
    {
        unordered_set<int> set;
        if(nums.size()==1)
        {
            return nums[0];
        }
        for(auto&e:nums)
        {
            if(set.find(e)==set.end())//not found
            {
                set.emplace(e);
            }
            else
            {
                set.erase(e);
            }
            

        }
        auto it = set.begin();
        return *it;
        
    }
};
```



다른 사람이 어떻게 해결했는지 궁금해서 찾아보니 XOR을 사용해서 해결하였다. 



**핵심으로 알아야 하는 개념 : **

<span style="background-color:#ffce55">xor은 입력값이 서로 같지 않을때 true이다 XOR 비트 연산을 사용하면 중복되지 않는 숫자를 남길수있다. 이때 중복이란 짝수횟수의 중복을 의미 한다 홀수 횟수의 중복은 감지 못한다.  어쨌든 xor연산을 사용하면 중복하는 숫자를 제거 하고 중복하지 않는 숫자를 남길수가 있다 </span>







```c++
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        int xorr=0;
        for(int i=0; i<nums.size(); i++){
            xorr=xorr^nums[i];
        }
        return xorr;
    }
};
```



코드가 훨신 간편해 졌다. 

