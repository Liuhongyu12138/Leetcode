### leetcode 6 Z字形变换

将一个给定字符串根据给定的行数，以从上往下、从左到右进行 Z 字形排列。

比如输入字符串为 "LEETCODEISHIRING" 行数为 3 时，排列如下：

L    C     I     R
E T O E S  I  I  G
E    D    H    N
之后，你的输出需要从左往右逐行读取，产生出一个新的字符串，比如："LCIRETOESIIGEDHN"。

请你实现这个将字符串进行指定行数变换的函数：

string convert(string s, int numRows);
示例 1:

~~~
输入: s = "LEETCODEISHIRING", numRows = 3
输出: "LCIRETOESIIGEDHN"
~~~


示例 2:

~~~
输入: s = "LEETCODEISHIRING", numRows = 4
输出: "LDREOEIIECIHNTSG"
解释:

L       D       R
E   O E    I   I
E C    I  H   N
T       S       G
~~~

题解

~~~python
"""
模拟法，很有意思的策略，如果行数为3，构建一个list其中三个空字符串，["", "", ""]
依次遍历每个字符，第一个字符放第一个字符串，第二个字符放第二个字符串，第三个字符放第三个字符串，
第四个字符放第二个字符串。控制两个变量，row表示当前字符放在第几行，flag表示遍历方向。
最后得到三个字符串直接依次拼接就可以了。
"""
class Solution:
    def convert(self, s: str, numRows: int) -> str:
        if numRows < 2:
            return s
        
        res = [""] * numRows
        
        row, flag = 0, -1
        
        for c in s:
            res[row] += c
            if row == 0 or row == numRows-1:
                flag = -flag
            
            row += flag
        
        return "".join(res)
~~~



