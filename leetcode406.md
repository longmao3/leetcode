[leetcode406](https://leetcode-cn.com/problems/queue-reconstruction-by-height/)

参考官方解答

贪心算法：每一步（局部）都更根据最优策略来执行，直到全局最优。

```java
class Solution {
    public int[][] reconstructQueue(int[][] people) {
       Arrays.sort(people,(o1,o2) ->
                o1[0]==o2[0]?o1[1]-o2[1]:o2[0]-o1[0]
        );
        List<int[]> list = new LinkedList<>();
        for(int[] p : people){
            list.add(p[1],p);
        }
        return list.toArray(new int[people.length][2]);
    }
}
```

