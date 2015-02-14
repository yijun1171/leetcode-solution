**时间**:2015.2.14

**问题描述**:括号匹配,字符串中只包含"{}[]()",这六种字符

example:

1. input:"{[})" output:false
2. input:"{}[]" output:true

**code**:
```java
 class ValidParentheses {
    Set set = new HashSet(Arrays.asList(')','}',']'));
    public boolean isValid(String s) {
        Stack stack = new Stack();
        char[] array = s.toCharArray();
        for (int i = 0; i < array.length; i++){
            if(set.contains(array[i])){
                if(stack.size() < 1)
                    return false;
                Character top = (Character) stack.pop();
                boolean flag = true;
                switch (array[i]) {
                    case ')': flag = top == '('; break;
                    case '}': flag = top == '{'; break;
                    case ']': flag = top == '['; break;
                }
                if(!flag)
                    return false;
            } else {
                stack.push(array[i]);
            }
        }
        return stack.empty();
    }

    public static void main(String[] args){
        ValidParentheses test = new ValidParentheses();
        System.out.println(test.isValid("[]"));
        System.out.println(test.isValid("["));
        System.out.println(test.isValid("()"));
        System.out.println(test.isValid("()[]{}"));
        System.out.println(test.isValid("(]"));
        System.out.println(test.isValid("([)]"));
    }  

```
**思路**:
很简单,使用栈,只需要遇到正括号入栈,遇到反括号,查看栈顶符号是否匹配,匹配时弹栈,不匹配返回false.注意字符串扫描结束后检查栈是否为空,不为空时返回false.
