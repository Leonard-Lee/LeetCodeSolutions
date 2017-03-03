### Question Title
- [339. Nested List Weight Sum](https://leetcode.com/problems/nested-list-weight-sum/)

### Question Description
> Given a nested list of integers, return the sum of all integers in the list weighted by their depth.
>
> Each element is either an integer, or a list -- whose elements may also be integers or other lists.
>
> Example 1:
> Given the list [[1,1],2,[1,1]], return 10. (four 1's at depth 2, one 2 at depth 1)
>
> Example 2:
> Given the list [1,[4,[6]]], return 27. (one 1 at depth 1, one 4 at depth 2, and one 6 at depth 3; 1 + 4*2 + 6*3 = 27)


### Question Type
- [x] DFS BFS

### Follow Up
- (1)Recursion DFS, (2)Iteration DFS, (3)Iteration BFS

---------------------------------------------------------------------------
# [Solution 1 - Recursion DFS]


### Thoughts
Using Recursion

### Complexity
- Time:  O(V)
- Space:


### Ref Links


### Source Code
```python
    def depthSum(self, nestedList):
        """
        :type nestedList: List[NestedInteger]
        :rtype: int
        """
        return self.helper(nestedList, 1)

    def helper(self, list, depth):
        sum = 0
        for ni in list:
            if ni.isInteger():
                sum += ni.getInteger() * depth
            else:
                sum += self.helper(ni.getList(), depth+1)    
        return sum
```


---------------------------------------------------------------------------
# [Solution 2 - Iteration DFS]


### Thoughts
Using Iteration + Stack

Also use tuple to combine Depth with NestedInteger

### Complexity
- Time:  O(V)
- Space:


### Ref Links


### Source Code
```python
def depthSum(self, nestedList):
        sum = 0
        stack = []
        stack.append((nestedList, 1))
        while stack:
            list, depth = stack.pop()
            for ni in list:
                if ni.isInteger():
                    sum += ni.getInteger() * depth
                else:
                    stack.append((ni.getList(), depth+1))

        return sum
```


---------------------------------------------------------------------------
# [Solution 3 - Iteration BFS]


### Thoughts
Using Iteration + Queue

這裡作法蠻巧妙的，在while dq:，
不是只有一次pop，而是有多次pop，同一層有幾個就pop幾個，
所以當離開 while dq:中的for loop時，就到了下一層了

### Complexity
- Time:  O(V)
- Space:


### Ref Links


### Source Code
```python
def depthSum(self, nestedList):
        sum = 0
        depth = 1
        dq = collections.deque()
        dq.append(nestedList)

        while dq:
            for i in xrange(len(dq)):
                list = dq.popleft()

                for ni in list:
                    if ni.isInteger():
                        sum += ni.getInteger() * depth
                    else:
                        dq.append(ni.getList())

            depth += 1

        return sum
```
