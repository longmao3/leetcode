[leetcode56](https://leetcode-cn.com/problems/merge-intervals/submissions/)

先将数组进行排序。

* 对于数组，排序是一个常规思路。

```java
public int[][] merge(int[][] intervals) {
    List<int[]> res = new ArrayList<>();
    if (intervals.length == 0)
        return res.toArray(new int[0][0]);
    Arrays.sort(intervals, new Comparator<int[]>() {  //注意数组也可以作为泛型
        @Override
        public int compare(int[] o1, int[] o2) {
            return o1[0]-o2[0];
        }
    });

    int i = 0;
    while (i<intervals.length){
        int left = intervals[i][0];
        int right = intervals[i][1];
        while (i<intervals.length-1 && intervals[i+1][0]<=right) {
            right = Math.max(intervals[i + 1][1],right);
            i++;
        }
        res.add(new int[] {left,right});
        i++;
    }
    return res.toArray(new int[0][0]); //看源码
}
```