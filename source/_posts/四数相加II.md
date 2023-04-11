---
title: 4Sum II
date: 2023-04-11 16:13:51
tags:
---

## 四数相加II
给你四个整数数组 nums1、nums2、nums3 和 nums4 ，数组长度都是 n ，请你计算有多少个元组 (i, j, k, l) 能满足：
0 <= i, j, k, l < n
nums1[i] + nums2[j] + nums3[k] + nums4[l] == 0
```java
class Solution {
    public int fourSumCount(int[] nums1, int[] nums2, int[] nums3, int[] nums4) {
        HashMap<Integer, Integer> sum = new HashMap<>();
        for(int a : nums1){
            for(int b : nums2){
                sum.put(a + b, sum.getOrDefault(a + b, 0) + 1);
            }
        }
        int ans = 0;
        for(int a : nums3){
            for(int b : nums4){
                if(sum.containsKey(- a - b)){
                    ans += sum.get(- a - b); 
                }
            }
        }
        return ans;
    }
}
```
先遍历`nums1`、`nums1`将和为`a + b`的结果的个数放入map，在遍历`nums3`、`nums4`检查map中是否有`- a - b`，若有加入返回值