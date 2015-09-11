**时间**:2015.9.11

**问题描述**:Given a triangle, find the minimum path sum from top to bottom. Each step you may move to adjacent numbers on the row below.

**要求**: 
input:
[
     [2],
    [3,4],
   [6,5,7],
  [4,1,8,3]
]

output:11 (i.e., 2 + 3 + 5 + 1 = 11)

**code**:
```java
     /**
     * bottom-up DP方法
     * 最优子结构：对于k层i节点 知道了[K+1][i] [K+1][i+1] 两个节点的最短路径和 也就知道了k层i节点的最短路径和
     * 重叠子问题：从下往上计算的时候，下面的节点路径和都会被用到
     * @param triangle
     * @return
     */
    public int minimumTotalDP(List<List<Integer>> triangle) {
        int height = triangle.size();
        Integer[] mins = new Integer[height];
        mins = triangle.get(height-1).toArray(mins);
        for (int layer = height - 2; layer >= 0; layer--) {
            for (int index = 0; index <= layer; index ++) {
                mins[index] = Math.min(mins[index], mins[index+1])
                        + triangle.get(layer).get(index);
            }
        }

        return mins[0];
    }

    //贪心的思路 失败的解法
    //top-bottom 只能拿到局部最优 不能拿到全局最优
    public int minimumTotal(List<List<Integer>> triangle) {
        if(triangle == null || triangle.size() == 0)
            return 0;
        int height = triangle.size();
        int result = 0;
        int pos = 0;
        for(int layer = 0; layer < height; layer++){
            if(layer == 0)
                pos = 0;
            result += triangle.get(layer).get(pos);

            if(layer == height - 1)//到达最后一层
                break;
            pos = nextStep(pos, triangle.get(layer+1));
        }

        return result;
    }

```

**思路**：
典型的动态规划，一开始还没看出来。最开始的直觉是贪心，自上而下，每次找到下层相邻节点的最小值。结果后果就是每次拿到的是局部最优。
