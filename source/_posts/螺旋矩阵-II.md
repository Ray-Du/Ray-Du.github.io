---
title: 螺旋矩阵 II
date: 2023-04-06 22:48:06
tags:
---

## 螺旋矩阵 II
给你一个正整数 n ，生成一个包含 1 到 n2 所有元素，且元素按顺时针顺序螺旋排列的 n x n 正方形矩阵 matrix 。
```java
class Solution {
    public int[][] generateMatrix(int n) {
        int l = 0, r = n - 1, t = 0, b = n - 1;
        int start = 1, end = n * n;
        int[][] ans = new int[n][n];
        while(start <= end){
            for(int i = l; i <= r; i++) ans[t][i] = start++;
            t++;
            for(int i = t; i <= b; i++) ans[i][r] = start++;
            r--;
            for(int i = r; i >= l; i--) ans[b][i] = start++;
            b--;
            for(int i = b; i >= t; i--) ans[i][l] = start++;
            l++;
        }
        return ans;
    }
}
```
本体难点在于确定起始位置以及终止位置，模拟过程分别为：`for(int i = l; i <= r; i++)`从左往右（这里由于顶部放完了，因此后续顶部永久下降`t++`），`for(int i = t; i <= b; i++)`从上往下（这里由于右侧放完了，因此后续右侧永久左移`r--`），`for(int i = r; i >= l; i--)`从右往左（这里由于底部放完了，因此后续底部永久上移`b++`），`for(int i = b; i >= t; i--)`从下往上（这里由于左侧放完了，因此后续左侧永久右移`l++`），重复下一个`while`循环
