[leetcode56](https://leetcode-cn.com/problems/merge-intervals/)

```java
class Solution {
    public int[][] merge(int[][] intervals) {
         ArrayList<int[]> res = new ArrayList<>(); //int[]也可以被放倒list里面
        if(intervals.length == 0 )
            return new int[0][0];
    
        //排序//其实这里并不需要再按照结尾进行排序了，起始点相同的两个区段之间的顺序并不重要。
        Arrays.sort(intervals,(o1,o2)->o1[0]==o2[0]?o1[1]-o2[1]:o1[0]-o2[0]);
        //初始化。
        int end = intervals[0][1];
        int start = intervals[0][0];
        for(int[] inter : intervals){
            if(inter[0] > end){
                res.add(new int[]{start,end});
                start=inter[0];
                end=inter[1];
            }else{
                end=Math.max(end,inter[1]);
            }
        }
        res.add(new int[]{start,end});
        return res.toArray(new int[res.size()][2]);
    }
}
```

