**时间**:2015.5.17

**问题描述**:3sum

Given an array S of n integers, are there elements a, b, c in S such that a + b + c = 0? Find all unique triplets in the array which gives the sum of zero.

Note:
Elements in a triplet (a,b,c) must be in non-descending order. (ie, a ≤ b ≤ c)
The solution set must not contain duplicate triplets.
    For example, given array S = {-1 0 1 2 -1 -4},

    A solution set is:
    (-1, 0, 1)
    (-1, -1, 2)

**code**:
```java
public List<List<Integer>> solution2(int[] nums){
        int len = nums.length;
        List<List<Integer>> result = new LinkedList<List<Integer>>();
        if(len < 3) return result;
        Arrays.sort(nums);
        int indexPositive = 0;
        for(int i = 0; i < len; i++){
            if(nums[i] >= 0) {
                indexPositive = i;
                break;
            }
        }//indexPositive保证第一个可能数是负数
		
        for(int a = 0; a < indexPositive; a++){
            if(a > 0 && nums[a] == nums[a-1])
                continue;
            int front = a+1, end = len-1;
            while (front < end){
                int sum = nums[front] + nums[end];
                if(sum == -nums[a]){
                    Integer[] item = {nums[a], nums[front], nums[end]};

                    if(front > 0 && end < len-1 && nums[front] == nums[front-1] && nums[end] == nums[end+1]) {//去重
                        front++;end--;
                        continue;
                    }
                    result.add(Arrays.asList(item));
                    front++;end--;
                }else {
                    if(sum <= -nums[a])
                        front++;
                    else
                        end--;
                }
            }
        }
        if(indexPositive+2<len && nums[indexPositive] == 0 && nums[indexPositive+1] == 0 && nums[indexPositive+2] == 0){
            Integer[] item = {0,0,0};
            result.add(Arrays.asList(item));
        }
        return result;
    }

```
总体思想是先排序，然后从小到大枚举所有的非正数。
枚举过程中，假设正在枚举的数是a，那么在大于a的子数组中寻找sum=-a的两个数b,c.(sum=b+c,b>a,c>a)
寻找sum的过程，用两个指针分别指向子数组的首尾，向中间搜索
要注意某些边界问题，输入中可能会出现[0,0,0]的情况