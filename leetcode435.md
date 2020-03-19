[leetcode435](https://leetcode-cn.com/problems/non-overlapping-intervals/)

1.  数组问题常用解决套路就是排序。
2. 此题就是要保证从第一个区间开始的位置，使得bound增长最慢。

```java
class Solution {
    public int eraseOverlapIntervals(int[][] intervals) {
        if(intervals.length == 0 || intervals.length == 1){
             return 0;
        }
        Arrays.sort(intervals,(o1,o2)-> o1[0] == o2[0]?o1[1]-o2[1]:o1[0]-o2[0]);  //
        int res = 0;
        int bound = intervals[0][1];
        int index = 1,length=intervals.length;
        while(index < length){
           if( intervals[index][0] < bound){
               res++; 
               bound = Math.min(bound,intervals[index][1]);//可能会去掉上面一个区间。
           }else{
               bound = intervals[index][1];
           }
            index++;
        }
        return res;

    }
}
```

