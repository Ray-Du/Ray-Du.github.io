---
title: implement strStr
date: 2023-04-24 13:55:59
tags:
---

## 找出字符串中第一个匹配项的下标
给你两个字符串 haystack 和 needle ，请你在 haystack 字符串中找出 needle 字符串的第一个匹配项的下标（下标从 0 开始）。如果 needle 不是 haystack 的一部分，则返回  -1 。
```java
class Solution {
    public int strStr(String haystack, String needle) {
        if(needle.length() == 0){
            return 0;
        }
        int[] next = new int[needle.length()];
        getNext(next, needle);
        int j = -1;
        for(int i = 0; i < haystack.length(); i++){
            while(j >= 0 && haystack.charAt(i) != needle.charAt(j + 1)){
                j = next[j];
            }
            if(haystack.charAt(i) == needle.charAt(j + 1)){
                j++;
            }
            if(j == (needle.length() - 1)){
                return (i - needle.length() + 1);
            }
        } 
        return -1;
    }

    private void getNext(int[] next, String s){
        int j = -1;
        next[0] = j;
        for(int i = 1; i < s.length(); i++){
            if(j >= 0 && s.charAt(i) != s.charAt(j + 1)){
                j = next[j];
            }
            if(s.charAt(i) == s.charAt(j + 1)){
                j++;
            }
            next[i] = j;
        }
    }
}
```
通过`getNext`构建next数组，描述`needle`字符串匹配到每个字符时下一次如果没匹配上应该回退几个字符，指向`haystack`的指针永不回退