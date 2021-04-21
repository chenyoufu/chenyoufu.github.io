---
title: "112 路径总和"
date: 2021-04-21T17:12:32+08:00
draft: false
tags: ["算法", "树"]
categories: ["技术"]
---

给你二叉树的根节点 root 和一个表示目标和的整数 targetSum ，判断该树中是否存在 根节点到叶子节点 的路径，这条路径上所有节点值相加等于目标和 targetSum 。

叶子节点 是指没有子节点的节点。

```
输入：root = [1,2,3], targetSum = 5
输出：false
```

链接：https://leetcode-cn.com/problems/path-sum

**解题思路**

**V1 递归 DFS** 

```python
class Solution(object):
    def hasPathSum(self, root, targetSum):
        if not root:
            return False # python的true和false都是大写开头
        
        sums = []
        self.helper(root, root.val, sums)
        for s in sums:
            if s == targetSum:
                return True
        return False
        
    def helper(self, root, s, sums):
        if not root.left and not root.right:
            sums.append(s)
        
        if root.left:
            self.helper(root.left, s + root.left.val, sums)
        if root.right:
            self.helper(root.right, s + root.right.val, sums)
```

**V2 优化**

```python
class Solution(object):
    def hasPathSum(self, root, targetSum):
        if not root:
            return False
        
        return self.helper(root, targetSum-root.val)
        
    def helper(self, root, targetSum):
        
        if not root.left and not root.right:
            return targetSum == 0
        
        v1 = False
        v2 = False
        
        if root.left:
            v1 = self.helper(root.left, targetSum-root.left.val)
        if root.right:
            v2 = self.helper(root.right, targetSum-root.right.val)
        return v1 or v2
```

**V3 继续精简**

```python
class Solution(object):
    def hasPathSum(self, root, targetSum):
        if not root:
            return False
        
        if not root.left and not root.right:
            return targetSum == root.val
        
        return self.hasPathSum(root.left, targetSum-root.val) or self.hasPathSum(root.right, targetSum-root.val)
```

**V4 非递归DFS**

```python
class Solution(object):
    def hasPathSum(self, root, targetSum):
        if not root:
            return False

        stack = [(root, root.val)]

        while stack:
            node, v = stack.pop()
            if not node.left and not node.right and v == targetSum:
                return True
            
            if node.right:
                stack.append((node.right, v + node.right.val))
            
            if node.left:
                stack.append((node.left, v + node.left.val))

        return False
```