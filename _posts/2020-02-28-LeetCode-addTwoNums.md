---
layout: post
title:  "Coding LeetCode"
categories: algorithm
tags:  链表
author: LWL
---

* content
{:toc}

## 题目：两数相加

给出两个 非空 的链表用来表示两个非负的整数。其中，它们各自的位数是按照 逆序 的方式存储的，并且它们的每个节点只能存储 一位 数字。

如果，我们将这两个数相加起来，则会返回一个新的链表来表示它们的和。

您可以假设除了数字 0 之外，这两个数都不会以 0 开头。

You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

**示例：**

```
输入：(2 -> 4 -> 3) + (5 -> 6 -> 4)
输出：7 -> 0 -> 8
原因：342 + 465 = 807
```



## Python：

```python
class Solution:
    def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
        list1 = []
        list2 = []
        while l1:
            list1.append(str(l1.val))
            l1 = l1.next
        while l2:
            list2.append(str(l2.val))
            l2 = l2.next       
        num1 = int(''.join(list1[::-1]))
        num2 = int(''.join(list2[::-1]))
        num = list(str(num1 + num2))
        num = num[::-1]
        res = [int(i) for i in num]
        res_ = ListNode(0)
        l3 = res_
        for i in res:
            l3.next = ListNode(i)
            l3 = l3.next    
        return res_.next
```



- 上述代码用了投机取巧的方法，把两个链表里面的数拿出来进行数学上的相加。然后将相加的数再转换成链表。效率还可以。

```python
class Solution:
    def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
        # 定义一个进位标志
        a,b,p,carry = l1,l2,None,0
        while a or b:
            # a和b节点的值相加，如果有进位还要加上进位的值
            val = (a.val if a else 0)+(b.val if b else 0)+carry
            # 根据val判断是否有进位,不管有没有进位，val都应该小于10
            carry,val = val//10 if val>=10 else 0,val%10
            p,p.val = a if a else b,val
            # a和b指针都前进一位
            a,b = a.next if a else None,b.next if b else None
            # 根据a和b是否为空，p指针也前进一位
            p.next = a if a else b
        # 不要忘记最后的边界条件，如果循环结束carry>0说明有进位需要处理这个条件	
        if carry:
            p.next = ListNode(carry)
        # 每次迭代实际上都是将val赋给a指针的，所以最后返回的是l1	
        return l1
```



- 上述代码是用链表实现，比较重要的是carry进位值记录指针，这个指针的引进是效率提升以及代码简化的关键。当初自己写的时候没有引进这个指针导致代码比较长（多写了一些判断），效率也不及以上

## Go：

```golang
func addTwoNumbers(l1 *ListNode, l2 *ListNode) *ListNode {
	var result *ListNode
	next := &result
	num := 0
	for l1 != nil || l2 != nil || num > 0{
		if l1 != nil {
			num += l1.Val
			l1 = l1.Next
		}
		if l2 != nil {
			num += l2.Val
			l2 = l2.Next
		}
		*next = &ListNode{
			Val : num % 10,
			Next : nil,
		}
		num = num / 10
		next = &((*next).Next)
	}
	return result
}
```

- python第二种方法的重写






