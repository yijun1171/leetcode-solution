**时间**:2015.2.9

**问题描述**:比较版本号的大小(0.1 < 1.1 < 1.2 < 13.37),返回值与compareTo()方法一致

example. input:"1.10","1.11" output:-1

**code**:
```java
class CompareVersionNumber {

    public static int compareVersion(String version1, String version2){
        String[] levels1 = version1.split("\\.");
        String[] levels2 = version2.split("\\.");
        int maxLen = Math.max(levels1.length, levels2.length);

        for(int i = 0; i < maxLen; i++){
            Integer val1 = i < levels1.length ? Integer.parseInt(levels1[i]) : 0;
            Integer val2 = i < levels2.length ? Integer.parseInt(levels2[i]) : 0;
            int result = val1.compareTo(val2);
            if(result != 0)
                return result;
        }
        return 0;
    }

    public static void main(String[] args){
        System.out.println(compareVersion("1.2", "1.10"));
    }  
}

```
**思路**:
**注意**:分隔符左右两边的大小关系都是实数关系,很容易让人走入误区.例如"10.2"<"10.10".

将输入按'.'符号分割,再转换成Integer对象进行比较,jdk的实现处理了所有边界情况.例如"0000","001.230"
