**时间**:2015.2.9

**问题描述**:

原文描述的不够清晰,解释如下.

给定一个序列:1, 11, 21, 1211, 111221, ... 除了第一个数字,每个数字都是基于前一个数字构造出来的.

例如:
1. 11是基于1构造,1中只有**一**个**1**,因此**一 1** -> 11
2. 21是基于11构造,11中有**两**个**1**,因此**两 1** -> 21
3. 1211基于21构造,21中有**一**个**2**,紧跟着**一**个**1**,因此**一 2 一 1** -> 1211
依次递增,求出第n个位置的数字

example. input:5 output:111221

**code**:
```java
public static String countAndSay(int n){
        String lastNum  = "1";
        for(int i  = 1; i <= n - 1 ; i++){
            StringBuilder sb = new StringBuilder();
            char[] chars = lastNum.toCharArray();
            char cur = chars[0];
            int times = 0;
            for(int j = 0; j < lastNum.length(); j++){
                if(chars[j] == cur)
                    times ++;
                else {
                    sb.append(times).append(cur);
                    cur = chars[j];
                    times = 1;
                }
                if(j == lastNum.length() - 1){
                    sb.append(times).append(cur);
                }
            }
            lastNum = sb.toString();
        }
        return lastNum;
    }
```
**思路**:
每个数字连续出现的次数而已,注意不要忘了最后一组即可
