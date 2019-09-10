### leetcode 14 最长公共前缀

编写一个函数来查找字符串数组中的最长公共前缀。

如果不存在公共前缀，返回空字符串 ""。

示例 1:

~~~
输入: ["flower","flow","flight"]
输出: "fl"
~~~


示例 2:

~~~
输入: ["dog","racecar","car"]
输出: ""
解释: 输入不存在公共前缀。
~~~



说明:

所有输入只包含小写字母 a-z 。

题解

~~~python
"""
先选出最短的字符串，然后依次遍历这个字符串，和其他字符串的对应位置做比对，如果不一致，则return之前的子字符串。
"""
class Solution:
    def longestCommonPrefix(self, strs: List[str]) -> str:
        if not strs:
            return ""
        
        min_string = min(strs, key=len)
        
        for i in range(len(min_string)):
            for s in strs:
                if min_string[i] != s[i]:
                    return min_string[:i]
        
        return min_string
~~~

