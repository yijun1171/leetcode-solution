**时间**:2015.2.6

**问题描述**:求最长无重复字符子串的长度

**example1**:input:abcabcabc output:3

**example2**input:eee output:1

**code**:
```java  
  public int solution(String s) {
    int len = 0;
    char[] chars = s.toCharArray();
    Map<Character,Integer> map = new HashMap<Character,Integer>();//保存当前字串中的每一个字符
    for(int i = 0, j = 0;j < s.length(); j++){
      if(!map.containsKey(chars[j])){//当前字符没有出现过,将字符加入hashtable
        map.put(chars[j], j);
      } else {//字符出现过,将子串的头更新到该字符上一次出现的位置的下一位
        int temp = map.get(chars[j]) ;//上一次出现的位置
        map.put(chars[j], j);//更新字符出现的位置
        for(int x = i; x < temp; x ++){//移除不存在于子串中的符号
          map.remove(chars[x]);
        }
        i = temp + 1;//更新子串的头
      }
      if(len < map.size())
        len = map.size();
    }
    return len;
}
```
**思路**:
1. 表示:两个指针分别指向当前子串的首尾;**hashtable**用来保存子串中的所有符号:**key**:符号,**value**:符号的位置;子串长度等于**hashtable**的大小
2. 处理过程:
  子串的尾指针向后扫描:
  - 如果当前字符和子串不重复,则加入**hashtabe**;
  - 如果重复:
    - 将子串的指针头更新为该重复字符上一次出现的位置的**下一位**
    - 将不存在于更新后的子串中的符号,从**hashtable**中清除,使用一次遍历
    - 更新该重复子串出现的位置

**O(n)方法**:

```cpp
class Solution {
    public:
        int lengthOfLongestSubstring(string s) {
            if(s.size()<2) return s.size();
            int d=1, maxLen=1;
            unordered_map<char,int> map;
            map[s[0]]=0;
            for(int i=1;i<s.size();i++)
            {
                if(map.count(s[i])==0 || map[s[i]]<i-d)
                    d++;
                else
                    d= i- map[s[i]];
                map[s[i]]=i;
                if(d>maxLen)
                    maxLen = d;
            }
            return maxLen;
        }
    };
```
大致思想相同,优化的地方在于不用清除hashtable中不存在于子串中的符号,而在判断的时候,查看该符号上次出现的位置是不是在子串之中.
