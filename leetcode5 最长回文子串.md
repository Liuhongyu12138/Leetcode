### leetcode 5 最长回文子串

给定一个字符串 s，找到 s 中最长的回文子串。你可以假设 s 的最大长度为 1000。

示例 1：

~~~
输入: "babad"
输出: "bab"
注意: "aba" 也是一个有效答案。
~~~


示例 2：

~~~
输入: "cbbd"
输出: "bb"
~~~

题解1

~~~python
"""
比较简单的遍历法，遍历以每个点为中心点的结果，注意有可能是偶数回文，也有可能是奇数回文。
用i遍历字符串的每个位置，以i为中心点，j，k遍历回文位置。
"""
class Solution:
    def longestPalindrome(self, s: str) -> str:
        res = ""
        
        for i in range(len(s)):
            j, k = i, i
            while j >= 0 and k < len(s) and s[j] == s[k]:
                j -= 1
                k += 1
            if k-j-1 > len(res):
                res = s[j+1:k]
                
            j, k = i, i+1
            while j >= 0 and k < len(s) and s[j] == s[k]:
                j -= 1
                k += 1
            if k-j-1 > len(res):
                res = s[j+1:k]
        
        return res

~~~



题解2

~~~python
"""
动态规划：
1、状态表示：dp[i][j]:表示区间[i, j]是否是回文子串，True or False
2、状态转移：如果s[i] == s[j], dp[i][j] = dp[i+1][j-1] 	或者如果i,j已经是j-i<=2
           如果不等 直接False
"""
class Solution:
    def longestPalindrome(self, s: str) -> str:
        m = len(s)
        if m == 0:
            return ""
        
        res = s[0]
        dp = [[False] * m for _ in range(m)]
        
        for j in range(m):
            for i in range(j):
                dp[i][j] = s[i] == s[j] and (dp[i+1][j-1] or j-i<=2)
                
                if dp[i][j]:
                    if j-i+1 > len(res):
                        res = s[i:j+1]
        
        return res
~~~

