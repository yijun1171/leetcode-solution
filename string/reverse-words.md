**时间**:2015.2.10

**问题描述**:将字符串中的单词顺序翻转

example. input:" the sky is blue" output:"blue is sky the"

**code**:
```java
public class ReverseWords {

    public static String reverseWords(String s){
        String[] array = s.trim().split(" ");
        StringBuilder sb = new StringBuilder();
        for(int i = array.length - 1; i >= 0; i--){
            if(array[i].equals(""))
                continue;
            sb.append(array[i]);
            if(i != 0)
                sb.append(" ");
        }
        return sb.toString();
    }
}
```
**思路**:
将输入按空格分割,反向组合即可
注意:
1. 输入的首尾会出现空格,输出的首尾不能有空格
2. 输入的单词之间可能不止一个空格,输出的单词之间只能有一个空格
