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

# [剑指 Offer II 084. 含有重复元素集合的全排列 ](https://leetcode-cn.com/problems/7p8L0Z/)

**medium**

细节没处理好然后越来越乱，发现到头来自己思路出了问题

核心思路就是，保持每个位置相同的数字只能出现一次即可。

咱自己写的题解

![image-20220121015526211](https://s2.loli.net/2022/01/21/56uxcRhSBOeso3j.png)

```c++
class Solution {
public:
    vector<vector<int>> ans ;
    int n = 0 ;

    vector<vector<int>> permuteUnique(vector<int>& nums) {
        sort(nums.begin(), nums.end()) ;
        n = nums.size() ;
        DFS(nums, 0) ;
        return ans;
    }

    void DFS(vector<int> temp_ans, int index) 
    {
        if(index >= n) return ;
        if(index == n-1)
        {
            ans.emplace_back(temp_ans) ;
            return ;
        }
        for(int i = index ; i < n ; ++ i)
        {
            if(i != index && temp_ans[i] == temp_ans[index]) continue ;
            swap(temp_ans[index], temp_ans[i]) ;
            DFS(temp_ans, index+1) ;
        }
    }
};
```

# [剑指 Offer II 005. 单词长度的最大乘积](https://leetcode-cn.com/problems/aseY1I/)

**medium**

a-z 代表二进制位上从低位到高位

如果i-th个字符串有相应的单词，那么相应进制位即为1

处理过后，两个没有相同字符的字符串&的结果应为0

```c++
class Solution {
public:
    int maxProduct(vector<string>& words) {
        int n = words.size() ;
        vector<int> hash(n,0) ;
        for(int i = 0 ; i < n ; ++ i)
        {
            for(char const x : words[i])
            {
                hash[i] |= (1 << (x - 'a')) ;
            }
        }
        int maxx = 0 ;
        for(int i = 0 ; i < n ; ++ i)
        {
            int len1 = words[i].length() ;
            for(int j = i + 1 ; j < n ; ++ j)
            {
                int len2 = words[j].length() ;
                if(!(hash[i] & hash[j])) maxx = max(maxx, len1 * len2) ;
            }
        }
        return maxx ;
    }
};
```

