---
title: "167 两数之和 II - 输入有序数组"
date: 2021-06-07T22:43:35+08:00
draft: false
tags: ["算法", "数组"]
categories: ["技术"]
---

**题目**

给定一个已按照 升序排列  的整数数组 numbers ，请你从数组中找出两个数满足相加之和等于目标数 target 。

函数应该以长度为 2 的整数数组的形式返回这两个数的下标值。numbers 的下标 从 1 开始计数 ，所以答案数组应当满足 1 <= answer[0] < answer[1] <= numbers.length 。

你可以假设每个输入只对应唯一的答案，而且你不可以重复使用相同的元素。

 
示例 1：
```
输入：numbers = [2,7,11,15], target = 9
输出：[1,2]
解释：2 与 7 之和等于目标数 9 。因此 index1 = 1, index2 = 2 。
```

链接：https://leetcode-cn.com/problems/two-sum-ii-input-array-is-sorted

**解题思路**

* 下标从1开始计数

```python
class Solution(object):
    def twoSum(self, numbers, target):
        left = 0
        right = len(numbers) - 1
        while left < right:
            if numbers[left] + numbers[right] == target:
                return [left+1, right+1]
            elif numbers[left] + numbers[right] < target:
                left += 1 # 让sum大一些
            else:
                right -= 1 # 让sum小一些
        return None
```