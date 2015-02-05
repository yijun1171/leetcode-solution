**时间**:2015.2.4

**问题描述**:数字翻转

**example1**:input:123 output:321

**example2**input:-123 output:-321

**code**:
```java  
    public class solution {
      public int reverse(int x) {
    
      int n = x < 0 ? -x:x;
    
      int s=0;
    
      while(n > 0){
        int number = n % 10;
        if(Integer.MAX_VALUE / 10 < s)
          return 0;
      
        s = s * 10;
      
        if(Integer.MAX_VALUE - number < s)
          return 0;
    
      s = s + number;
      n = n / 10;
      
      }
    
      if(x < 0)
      s = -s;
      return s;
      }
    }
```
