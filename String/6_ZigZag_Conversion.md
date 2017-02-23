### Owner
- Stephen

### Question Title
- [295. Find Median from Data Stream](https://leetcode.com/problems/find-median-from-data-stream/?tab=Description/)

### Question Description
The string "PAYPALISHIRING" is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)

```
P   A   H   N
A P L S I I G
Y   I   R
```
And then read line by line: "PAHNAPLSIIGYIR"
Write the code that will take a string and make this conversion given a number of rows:
```
string convert(string text, int nRows);
```
convert("PAYPALISHIRING", 3) should return "PAHNAPLSIIGYIR".

### Question Type
- [x] String

### Follow Up
None

---------------------------------------------------------------------------
# [Solution 1]


### Thoughts
直接創造numRows個string去記錄每一列，使用for loop整個字串s，最後再把每一列合起來成一個字串return


### Complexity
- Time: O(len(s))+O(numRows),
- Space: O(numRows)


### Ref Links
-

### Source Code
```python
class Solution(object):
    def convert(self, s, numRows):
        """
        :type s: str
        :type numRows: int
        :rtype: str
        """
        if numRows == 1:
            return s

        index, step = 0, 1
        strList = [""] * numRows
        for c in s:
            strList[index] += c

            if index == 0:
                step = 1
            elif index == numRows - 1:
                step = -1

            index += step

        return "".join(strList)

```

---------------------------------------------------------------------------
# [Solution 2]


### Thoughts
直接for loop numRows次，直接把每一列裡的每一字找出來串起來；第一直行和第二直行的距離是space = numRows * 2 - 2；而中間斜上的字則是在1 ~ (numRows-2)列之間，距離為index + space - i * 2


### Complexity
- Time: O(numRows),
- Space: O(1)


### Ref Links
-

### Source Code
```python
class Solution(object):
    def convert(self, s, numRows):
        """
        :type s: str
        :type numRows: int
        :rtype: str
        """
        if numRows == 1:
            return s

        res = ""
        space = numRows * 2 - 2

        for i in xrange(numRows):
            index = i
            while index < len(s):
                res += s[index]

                if i > 0 and i < numRows - 1 and index + space - i * 2 < len(s):
                    res += s[index + space - i * 2]

                index += space

        return res

```
