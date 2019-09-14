### leetcode 17 电话号码的字母组合

给定一个仅包含数字 **2-9** 的字符串，返回所有它能表示的字母组合。

给出数字到字母的映射如下（与电话按键相同）。注意 **1** 不对应任何字母。

![image-20190914234504015](/Users/liuhongyu/Library/Application Support/typora-user-images/image-20190914234504015.png)

示例:

~~~
输入："23"
输出：["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].
~~~

说明:
尽管上面的答案是按字典序排列的，但是你可以任意选择答案输出的顺序。

题解：

~~~python
"""
基础dfs题，dfs题想好初始状态和终止状态就行，一般都会传入一个index=0 来作为终止条件。另外注意回朔。
当满足终止条件时，直接返回，或者将当前结果存储在res中。
本题传入digits，当前字符串，index。
当index=len(digits)时，将当前字符串加入到结果中。
"""
class Solution:
    def letterCombinations(self, digits: str) -> List[str]:
        self.dic = {
            '2': 'abc',
            '3': 'def',
            '4': 'ghi',
            '5': 'jkl',
            '6': 'mno',
            '7': 'pqrs',
            '8': 'tuv',
            '9': 'wxyz'
        }
        if not digits:
            return []
        
        self.res = []
        
        self.dfs(digits, '', 0)
        
        return self.res
    
    def dfs(self, digits, cur, index):
        if index == len(digits):
            self.res.append(cur)
            return 
        
        for a in self.dic[digits[index]]:
            cur += a
            self.dfs(digits, cur, index+1)
            cur = cur[:-1]
~~~



