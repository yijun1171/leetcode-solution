**时间**:2015.2.14

**问题描述**:回文判断,只判断字符串中的字母和数字部分(alphanumeric),忽略其他字符(包括空格),忽略大小写.

example:

1. input:"A man, a plan, a canal: Panama" output:true
2. input:"race a car" output:false

**code**:
```java

public class ValidPalindrome {

    public boolean isPalindrome(String s) {
        s = s.replaceAll(" ", "");
        s = s.toLowerCase();
        char[] array = s.toCharArray();
        for(int i = 0, j = array.length - 1; i <= j;){
            char head = array[i];
            char tail = array[j];
            if(Character.isLetterOrDigit(head)){
                i++;
                continue;
            }
            if(!Character.isLetterOrDigit(head)){
                j--;
                continue;
            }
            if(head != tail)
                return false;
            i++;
            j--;
        }
        return true;
    }

    public static void main(String[] args){
        ValidPalindrome test = new ValidPalindrome();
        System.out.println(test.isPalindrome("A man, a plan, a canal: Panama"));
        System.out.println(test.isPalindrome("race a car"));
    }
}
```
**思路**:

用两个指针从首尾向中间扫描

1. 去掉空格,全部转化为小写
2. 判断是否是alphanumberic
3. 判断是否相同

看了讨论区的其他思路,印象比较深的是使用正则表达式`[^0-9a-zA-Z]`,忽略不满足的字符
