---
title: Maximum Depth of N-ary Tree
date: 2023-04-24 16:22:12
tags:
---

## n叉树的最大深度
给定一个 N 叉树，找到其最大深度。
最大深度是指从根节点到最远叶子节点的最长路径上的节点总数。
N 叉树输入按层序遍历序列化表示，每组子节点由空值分隔。
```java
class Solution {
    public int maxDepth(Node root) {
        if(root == null){
            return 0;
        }
        int maxDepth = 0;
        for(Node node : root.children){
            maxDepth = Math.max(maxDepth(node), maxDepth);
        }
        maxDepth++;
        return maxDepth;
    }
}
```
二叉树经典递归，若当前结点为空时返回0，否则返回所有子树的最大深度，加上当前结点深度（1）