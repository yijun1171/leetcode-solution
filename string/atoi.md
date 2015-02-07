**时间**:2015.2.7

**问题描述**:实现atoi函数(将字符串转化成合法的整型)

**要求**:
1. 忽略字符串开头的所有空格
2. 正负号可选(-100,+100,100均合法)
3. 合法数字之后出现的其余符号将被忽略(98ab34 -> 98)
4. 第一个非空格字符不是数字;只包含空格;空串,都返回0
5. 溢出则返回上限值或者下限值

**code**:
```java  
    public static int atoi(String str){
        if(str.equals(""))//空串
            return 0;
        str = str.trim();
        if(str.equals(""))//只包含空格
            return 0;
        char[] arr = str.toCharArray();
        char zero = '0';
        char nine = '9';
        boolean flag = true;
        if(arr[0] == '-')
            flag = false;
        if(arr[0] == '-' || arr[0] == '+')
            arr = Arrays.copyOfRange(arr, 1, arr.length);
        int result = 0;
        for(int i = 0; i < arr.length; i++){
            if(arr[i] >= zero && arr[i] <= nine){//是数字
                int number = arr[i] - zero;
                if(Integer.MAX_VALUE / 10 < result)//溢出
                    return flag ? Integer.MAX_VALUE : Integer.MIN_VALUE;
                result = result * 10;
                if(Integer.MAX_VALUE - number < result)
                    return flag ? Integer.MAX_VALUE : Integer.MIN_VALUE;
                result = result + number;
            }else{
                break;
            }
        }
        return flag ? result : -result;
    }
```
**思路**:
主要考察所有的输入情况,实现并不难.合法数字的起点:去掉前置空格,正负号之后(optional)的第一个位置.该位置不是合法数字时,返回0,该位置之后出现的非法字符都会被忽略,而不是直接返回0
