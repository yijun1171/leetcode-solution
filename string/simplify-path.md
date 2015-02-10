**时间**:2015.2.10

**问题描述**:化简路径(unix-style)

example. input:"/home/../ac/b" output:"/ac/b"

**code**:
```java

public class SimplifyPath {

    public static String simplifyPath(String path){
        String[] array = path.split("/");
        Stack<String> stack = new Stack<String>();
        Set<String> skip = new HashSet(Arrays.asList("",".",".."));
        for(String s : array){
            if(s.equals("..") && !stack.isEmpty())
                stack.pop();
            else if(!skip.contains(s))
                stack.add(s);
        }
        StringBuilder sb = new StringBuilder();
        while(stack.size() > 0){
            sb.insert(0,stack.pop()).insert(0,"/");
        }
        return sb.length() == 0 ? "/" : sb.toString();
    }
}
```
**思路**:
将输入按**/**分割,用栈保存路径节点,遇到**..**且栈不空时弹栈,遇到节点时压栈,最后按序组合
注意:
1. 输入会出现各种奇怪的路径**///...**之类的,需要一个通用的处理方法
2. **/..**应该返回**/**
