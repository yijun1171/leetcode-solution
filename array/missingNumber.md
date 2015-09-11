**时间**:2015.9.11

**问题描述**:
 Given an array containing n distinct numbers taken from 0, 1, 2, ..., n,
 find the one that is missing from the array.

 For example,
 Given nums = [0, 1, 3] return 2.

 Note:
 Your algorithm should run in linear runtime complexity.
 Could you implement it using only constant extra space complexity?

**code**:
```java

    public int missingNumber(int[] nums) {
        int[] bitmap = new int[nums.length + 1];
        for(int i = 0; i < nums.length; i++){
            bitmap[nums[i]] = -1;
        }
        for(int i = 0; i < bitmap.length; i++){
            if(bitmap[i] != -1)
                return i;
        }
        return -1;
    }
```
**思路**：
使用位图，时间复杂度和空间复杂度都是O(N)。
看到一种更好的解法是利用异或，空间复杂度将到O(1)。伪码如下
```java
int x
for i in array
  x ^= i
  x ^= array[i]

return x
```
