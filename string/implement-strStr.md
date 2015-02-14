**问题描述**:实现strStr()函数(返回子串第一次出现的位置)

**要求**:
经典的字符串匹配题,子串不存在时返回-1,否则返回子串第一次出现的位置

example: input:"the sky is bule","sky" output:4
 
**code**:
```java  

```

**思路**:

1. 最容易想到的是暴力匹配(Bruce-force),从头扫描目标串和需要匹配的模式子串(pattern),不匹配时指针需要回溯.
2. KMP算法,经典但是理解和实现都比较复杂
3. [boyer-moore算法](http://www.ruanyifeng.com/blog/2013/05/boyer-moore_string_search_algorithm.html),效率高,构思巧妙.
4. Rabin-Karp算法,通过比较子串的hash值判断子串是否匹配 
