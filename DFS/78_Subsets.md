### Question Title
- [78. Subsets](https://leetcode.com/problems/subsets/?tab=Description)
- [90. Subsets II](https://leetcode.com/problems/subsets-ii/?tab=Description)

### Question Description
Given a set of distinct integers, nums, return all possible subsets.

Note: The solution set must not contain duplicate subsets.

For example,
If nums = [1,2,3], a solution is:

```
[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]
```

### Question Type
- [x] Array
- [x] Backtracking
- [x] DFS

### Follow Up
Given a collection of integers that might contain duplicates, nums, return all possible subsets.
Note: The solution set must not contain duplicate subsets.

For example,
If nums = [1,2,2], a solution is:

```
[
  [2],
  [1],
  [1,2,2],
  [2,2],
  [1,2],
  []
]
```
---------------------------------------------------------------------------
# [Solution of Subsets]


### Thoughts
在Tree中，同一層的走過不要再走了，所以同層left sibling是i+1；
而下一層也是index+1，parent node用過的數不能再用。

Subsets核心，DFS走過的每個node都是一個結果，要收到result裡


### Complexity
- Time:
- Space:


### Ref Links
-

### Source Code
```python
class Solution(object):
    def subsets(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        nums.sort()
        res = [[]]
        self.helper(nums, 0, [], res)
        return res

    def helper(self, nums, index, curList, res):
        for i in range(index, len(nums)):
            curList.append(nums[i])
            res.append(curList[:])
            self.helper(nums, i+1, curList, res)
            curList.pop()

```

---------------------------------------------------------------------------
# [Solution of Subsets II]


### Thoughts
排序，如果和同層的left sibling 數字相同就不做了；
要小心如果是每一層的第一個都要執行，避免被條件nums[i-1] == nums[i]刪去；
不使用nums[i+1:]，好寫，但效率不好，每次都new 一個新的陣列


### Complexity
- Time:
- Space:


### Ref Links
-

### Source Code
```python
class Solution(object):
    def subsetsWithDup(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        nums.sort()
        res = [[]]
        self.helper(nums, 0, [], res)
        return res

    # when not using nums[i+1:], it will be more efficent
    def helper(self, nums, index, curList, res):
        for i in xrange(index, len(nums)):
            if i == index or not (i > 0 and nums[i-1] == nums[i]):
                curList.append(nums[i])
                res.append(curList[:])
                self.helper(nums, i+1, curList, res)
                curList.pop()

```
