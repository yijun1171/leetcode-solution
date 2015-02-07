**问题描述**:判断一个数字是否回文

**example1**:input:123 output:false

**example2**input:123321 output:true

**code**:
```java  
public class PalindromeNumber {
    public static boolean isPalindrome(int x){
        if(x < 0)
            return false;
        if(x == reverse(x)){
            return true;
        }
        return false;
    }

    public static int reverse(int x) {

        int s=0;

        while(x > 0){
            int number = x % 10;
            if(Integer.MAX_VALUE / 10 < s)
                return -1;
            s = s * 10;
            if(Integer.MAX_VALUE - number < s)
                return -1;
            s = s + number;
            x = x / 10;
        }
        return s;
    }
}
```
**思路**:
将数字翻转然后判断是否和输入相同.需要考虑:
1. 负数不是回文
2. 处理翻转溢出的情况(翻转出现溢出说明输入本身就不是回文的)
