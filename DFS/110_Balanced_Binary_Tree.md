### Question Title
- [110. Balanced Binary Tree](https://leetcode.com/problems/balanced-binary-tree/)

### Question Description
> Given a binary tree, determine if it is height-balanced.

> For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.


### Question Type
- [x] DFS
- [x] Tree

### Follow Up
- (1)Recursion DFS, (2)正常解

---------------------------------------------------------------------------
# [Solution 1 - Recursion DFS]


### Thoughts
解法很技巧，把isBalanced()和height()結合起來，所以當檢查完高度也同時解查完是否balanced;
When the subtree is not balanced, return -1;
Or return the height of node

### Complexity
- Time:  O(V)
- Space:


### Ref Links


### Source Code
```python
class Solution(object):
  def height(self, node):
      if node is None:
          return 0

      lHeight = self.height(node.left)
      rHeight = self.height(node.right)

      if lHeight == -1 or rHeight == -1 or abs(lHeight - rHeight) > 1 :
          return -1
      else:
          return 1 + max(lHeight, rHeight)

  def isBalanced(self, root):
      """
      :type root: TreeNode
      :rtype: bool
      """
      return self.height(root) != -1
```


---------------------------------------------------------------------------
# [Solution 2 - 正常解]


### Thoughts
1. Check if the height of two subtrees differ more than 1
2. Check if left subtree is balanced
3. Check if right subtree is balanced

> Note. 可以把左右子樹的head是否為null丟到下一層再判斷，符合recursion general case，寫起來精簡漂亮； isBalanced()裡的getHeight()先行判斷，會比先判斷isBalanced()有效率多了
### Complexity
- Time:  O(V)
- Space:


### Ref Links


### Source Code
```python
class Solution(object):
    def isBalanced(self, root):
        """
        :type root: TreeNode
        :rtype: bool
        """
        if not root:
            return True
        else:
            return abs(self.getHeight(root.left) - self.getHeight(root.right)) < 2 and self.isBalanced(root.left) and self.isBalanced(root.right)

    def getHeight(self, node):
        if not node:
            return 0
        else:
            return 1 + max(self.getHeight(node.left), self.getHeight(node.right))
```
