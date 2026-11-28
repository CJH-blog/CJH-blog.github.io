---
categories: [算法]
title: 每日一题
subtitle: Largest Rectangle in Historgram
published: false
layout: post
author: 陈家辉
tags:
- algorithm

---

## Question

- [84. Largest Rectangle in Histogram](https://leetcode.com/problems/largest-rectangle-in-histogram/)

  

  Given an array of integers `heights` representing the histogram's bar height where the width of each bar is `1`, return *the area of the largest rectangle in the histogram*.

   

  **Example 1:**

  ![img](https://assets.leetcode.com/uploads/2021/01/04/histogram.jpg)

  ```
  Input: heights = [2,1,5,6,2,3]
  Output: 10
  Explanation: The above is a histogram where width of each bar is 1.
  The largest rectangle is shown in the red area, which has an area = 10 units.
  ```

  **Example 2:**

  ![img](https://assets.leetcode.com/uploads/2021/01/04/histogram-1.jpg)

  ```
  Input: heights = [2,4]
  Output: 4
  ```

   

  **Constraints:**

  - `1 <= heights.length <= 105`
  - `0 <= heights[i] <= 104`

## Intuition

To find the largest rectangle area, we need to determine for **each bar how far it can extend to the left and right**.

So the key is to find the left and right boundary of each bar.We can use monotonic stacks to compute the left boudary and right boundary seperately.

## Approach

1. Mataining monotonic stack to find the left and right boundary.
2. Before we put height into the stack, we should check the stack.peek(). If the stack is empty or the peek is smaller than current height, push it. Else it means this is right boundary, we should pop and compute the area.
3. The area = (i - peekValue-1)*heights[popValue]

## Code



```java
class Solution {
    public int largestRectangleArea(int[] heights) {
        int n = heights.length, ans = 0;
        Deque<Integer> stack = new ArrayDeque<>();
        for (int i = 0; i <= n; i++) {
            int cur = (i == n) ? 0 : heights[i];   // sentinel
            while (!stack.isEmpty() && cur < heights[stack.peek()]) {
                int h = heights[stack.pop()];
                int left = stack.isEmpty() ? -1 : stack.peek();
                int width = i - left - 1;
                ans = Math.max(ans, h * width);
            }
            stack.push(i);
        }
        return ans;
    }
}
```





