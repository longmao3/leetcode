[leetcode210](https://leetcode-cn.com/problems/course-schedule-ii/submissions/)

同 leetcode207

```java
//使用hashset 可以减少每次搜索的时间。
public static int[] findOrder(int numCourses, int[][] prerequisites) {
    int[] inDegrees = new int[numCourses];
    int[] res = new int[numCourses];
    int index=0;
    for(int[] pre :prerequisites) inDegrees[pre[0]]++;
    Queue<Integer> queue = new LinkedList<>();
    for (int i = 0; i < inDegrees.length; i++) {
        if (inDegrees[i] == 0)
            queue.offer(i);
    }
    while ( !queue.isEmpty()){
        Integer preNode = queue.poll();
        res[index] = preNode;
        index++;
        numCourses--;
        for (int[] pre : prerequisites){
            if (pre[1] == preNode){
                inDegrees[pre[0]]--;
                if (inDegrees[pre[0]] == 0)
                    queue.offer(pre[0]);
            }
        }
    }
    if( numCourses==0)
        return res;
    else
        return new int[0];
}
```