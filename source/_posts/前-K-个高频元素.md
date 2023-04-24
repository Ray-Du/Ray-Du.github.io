---
title: Top K Frequent Elements
date: 2023-04-24 15:16:25
tags:
---

## 前 K 个高频元素
给你一个整数数组 nums 和一个整数 k ，请你返回其中出现频率前 k 高的元素。你可以按任意顺序返回答案。
```java
class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        Map<Integer, Integer> frequency = new HashMap<>();
        for(int num : nums){
            frequency.put(num, frequency.getOrDefault(num, 0) + 1);
        }
        PriorityQueue<int[]> heap = new PriorityQueue<>((o1, o2) -> o1[1] - o2[1]);
        for(Map.Entry<Integer, Integer> entry : frequency.entrySet()){
            int num = entry.getKey(), cnt = entry.getValue();
            if(heap.size() == k){
                if(heap.peek()[1] < cnt){
                    heap.poll();
                    heap.offer(new int[]{num, cnt});
                }
            }else{
                heap.offer(new int[]{num, cnt});
            }
        }
        int[] ans = new int[k];
        for(int i = 0; i < k; i++){
            ans[i] = heap.poll()[0];
        }
        return ans;
    }
}
```
本题使用优先队列（堆排序）计算前k个高频元素，先使用`HashMap`获取元素频次，依次放入优先队列（小顶堆），每次到k弹出最小值，最后弹出k个值放入答案