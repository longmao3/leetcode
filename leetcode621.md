[leetcode621](https://leetcode-cn.com/problems/task-scheduler/submissions/)

参考[官方解法](https://leetcode-cn.com/problems/task-scheduler/solution/ren-wu-diao-du-qi-by-leetcode/)三，清晰，明白。

* 总时间=任务执行时间+空闲时间。

```java
class Solution {
    public int leastInterval(char[] tasks, int n) {
        int[] map = new int[26];
        for( int i=0;i<tasks.length;i++){
            map[tasks[i]-'A']++;
        }
        Arrays.sort(map);
        int max_val = map[25]-1,idel_slots=max_val*n;
        for(int i=24;i>=0 && map[i]>0;i--){
            idel_slots-=Math.min(max_val,map[i]);//防止出现，相等的情况。
        }
        return idel_slots>0?tasks.length+idel_slots:tasks.length;
    }
}
```

