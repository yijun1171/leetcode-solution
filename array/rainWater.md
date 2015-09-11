**时间**:2015.9.11

**问题描述**:

Given n non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it is able to trap after raining.

For example,
![](http://www.leetcode.com/wp-content/uploads/2012/08/rainwatertrap.png)
input : [0,1,0,2,1,0,1,3,2,1,2,1]
output: 6.

**code**:
```java
    /**
     * 从头向后搜索 记搜索起点为i，搜索指针为x
     * 1.遇到第一个height[x] => height[i] 搜索结束，右边界为x,容量由i决定，计算容量并更新i
     * 2.不是以上情况，记录遇到height[x]的最大值max，直到数组末尾。那么右边界为max的索引，容量由max决定，计算容量，更新i=pos of max
     * @param height
     * @return
     */
    public int trap(int[] height) {
        if(height == null || height.length == 0)
            return 0;

        int result = 0;
        int i = 0;
        //循环不变式：每次循环得到一次容量计算 并更新i的
        while(i < height.length - 1){
            if(height[i] == 0 || height[i] == height[i+1]){
                i++;
                continue;
            }
            int max = i + 1;//height[max] < height[i]；height[max] = max(height[x])

            for(int x = i + 1; x < height.length; x ++){
                if(height[i] <= height[x]){
                    result += cal(i+1, x-1, height[i], height);
                    i = x;
                    break;
                }
                else {
                    max = height[x] > height[max] ? x : max;
                    if(x == height.length - 1){
                        result += cal(i+1, max-1, height[max], height);
                        i = max;
                        break;
                    }
                }
            }
        }
        return result;
    }


    /**
     * 计算start~end中的容量
     * @param start
     * @param end
     * @param level 水位高度
     * @return
     */
    private int cal(int start, int end, int level, int[] height){
        int result = 0;
        for(int i = start; i <= end; i++){
            if(height[i] >= level)
                throw new IllegalArgumentException(String.format("height[%d] = %d", i, height[i]));
            result += level - height[i];
        }
        return result;
    }

```
**思路**：很直观的向前搜索
