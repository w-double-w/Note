# [剑指 Offer II 004. 只出现一次的数字 ](https://leetcode-cn.com/problems/WGki4K/)

**medium**

拿到手没思路啊！

看了题解发现是每个二进制位上统计，被一开始的线性时间复杂度误解到了，以为需要一次遍历就得出答案。

但是自己打了一遍错在了负数的样例，后来发现符号位没有统计进去。

```c++
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        int ans = 0 ;
        for(int i = 0 ; i < 32 ; ++ i)
        {
            int num = 0 ;
            for(auto const x : nums)
            {
                if((x >> i) & 1) num ++ ;
            }
            if(num % 3) ans |= (1<<i) ;
        }
        return ans ;
    }
};
```

