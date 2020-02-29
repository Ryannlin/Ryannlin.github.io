---
layout: post
title:  "Coding LeetCode"
categories: algorithm
tags:  双指针 SlidingWindow
author: LWL
---

* content
{:toc}

## 题目：无重复字符的最长子串

给定一个字符串，请你找出其中不含有重复字符的 **最长子串** 的长度。

Given a string, find the length of the longest substring without repeating characters.

**示例 1:**

```
输入: "abcabcbb"
输出: 3 
解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。
```

## Python：

```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        if not s:return 0
        length_s = len(s)
        res = 1
        start = 0  # 记录循环初始字符串位置
        end = 1    # 记录子串长度
        while start < length_s - end:
            for i in range(start,length_s-end):
                # 特判：当没有符合条件的子串时，终止while循环
                if i == length_s - end - 1 and len(set(s[i:end+1+i])) != len(s[i:end+1+i]):
                    return res
                if len(set(s[i:end+1+i])) == len(s[i:end+1+i]):
                    res += 1
                    start = i
                    break
            end += 1
        return res
```



- 循环里的特判条件是所有测试用例得以通过的原因，但是整体效率并不是很高。接下来介绍滑动窗口：

```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        if not s:return 0
        left = 0
        lookup = set() # 动态记录不重复子串
        n = len(s)
        max_len = 0
        cur_len = 0
        for i in range(n):
            cur_len += 1
            while s[i] in lookup:
                lookup.remove(s[left])
                left += 1
                cur_len -= 1
            if cur_len > max_len:max_len = cur_len
            lookup.add(s[i])
        return max_len
```



- 效率提升在动态更新set里面的元素，第一种方法是多次将list转换成set进行比较，相对耗时。

## Go：

```golang
func lengthOfLongestSubstring(s string) int {
	window, start := 0, 0
	for key := 0; key < len(s); key ++ {
		isExist := strings.Index(string(s[start:key]), string(s[key]))
		if (isExist == -1) {
			if (key - start + 1 > window) {
				window = key - start + 1
			} 
		}else {
			start = isExist + start + 1
		}
	}
	return window
}
```

- 不定长滑动窗口go解法，参考LeetCode上题解，代码量以及效率上有所提升。






