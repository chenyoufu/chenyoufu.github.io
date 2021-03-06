---
title: "141 环形链表"
date: 2021-05-30T09:30:45+08:00
draft: false
tags: ["算法", "链表"]
categories: ["技术"]
---

**题目**

给定一个链表，判断链表中是否有环。

如果链表中有某个节点，可以通过连续跟踪 next 指针再次到达，则链表中存在环。 为了表示给定链表中的环，我们使用整数 pos 来表示链表尾连接到链表中的位置（索引从 0 开始）。 如果 pos 是 -1，则在该链表中没有环。注意：pos 不作为参数进行传递，仅仅是为了标识链表的实际情况。

如果链表中存在环，则返回 true 。 否则，返回 false 。

**解题思路**

快慢指针

```go
func hasCycle(head *ListNode) bool {
    slow := head
    fast := head

    for slow != nil && fast != nil && fast.Next != nil { // 这个边界fast.Next不能忘记判断nil 
        slow = slow.Next
        fast = fast.Next.Next
        if slow == fast {
            return true
        }
    }

    return false
}
```