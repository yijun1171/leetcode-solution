**时间**:2015.2.8

**问题描述**:返回两个字符串的二进制和

**要求**:
example: intput:"100","1" output:"101"

**code**:
```java  
public class AddBinary {
    public static String addBinary(String a, String b) {
        char[] aChars = a.toCharArray();
        char[] bChars = b.toCharArray();
        int i = aChars.length - 1, j = bChars.length - 1;
        boolean carry = false;//进位
        StringBuilder result = new StringBuilder();
        for(;i >= 0 && j >=0 ; i--, j-- ){
            int temp = aChars[i] + bChars[j] - 2 * '0' + (carry ? 1 : 0);//一位运算的结果,取值为0,1,2,3
            result.append((char)('0' + temp % 2));//当前位的值
            carry = (temp - 2) >= 0;//进位
        }
        if(i - j > 0) {//a还有余下的位
            for(; i >=0 ; i--){
                int temp = aChars[i] - '0' + (carry ? 1 : 0);
                result.append((char)('0' + temp % 2));
                carry = (temp - 2) >= 0;
            }
        } else if(j - i > 0){
            for(; j >=0 ; j--){
                int temp = bChars[j] - '0' + (carry ? 1 : 0);
                result.append((char)('0' + temp % 2));
                carry = (temp - 2) >= 0;
            }
        }
        if(carry)
            result.append('1');
        result.reverse();
        return result.toString();
    }

    public static void main(String[] args) {
        System.out.println(addBinary("1", "1"));
    }
}
```
**思路**:
获得字符串的每一位值进行直接计算,简洁的办法是进行异或(XOR)计算

需要注意的几点:
1. 两个输入字符串长度不同时,如何优雅的处理几种不同的情况(自己实现的很丑陋--)
2. 两个输入字符串都遍历完成之后,需要加上最后一个进位的值

**一个好点的实现**
```java
public class Solution {
    public String addBinary(String a, String b) {
        if(a == null || a.isEmpty()) {
            return b;
        }
        if(b == null || b.isEmpty()) {
            return a;
        }
        char[] aArray = a.toCharArray();
        char[] bArray = b.toCharArray();
        StringBuilder stb = new StringBuilder();

        int i = aArray.length - 1;
        int j = bArray.length - 1;
        int aByte;
        int bByte;
        int carry = 0;
        int result;

        while(i > -1 || j > -1 || carry == 1) {
            aByte = (i > -1) ? Character.getNumericValue(aArray[i--]) : 0;//在这里处理了长度不同的情况
            bByte = (j > -1) ? Character.getNumericValue(bArray[j--]) : 0;
            result = aByte ^ bByte ^ carry;//异或运算更加简洁
            carry = ((aByte + bByte + carry) >= 2) ? 1 : 0;
            stb.append(result);
        }
        return stb.reverse().toString();
    }
}
```
