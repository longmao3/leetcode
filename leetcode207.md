[leetcode207](https://leetcode-cn.com/problems/course-schedule/)

​	深度广度优先搜索，每去除掉入度为零的节点

```java
public static boolean canFinish(int numCourses, int[][] prerequisites) {
    int[] inDegrees = new int[numCourses];
   for(int[] pre :prerequisites) inDegrees[pre[0]]++;
    Queue<Integer> queue = new LinkedList<>();
    for (int i = 0; i < inDegrees.length; i++) {  //建立入度表
        if (inDegrees[i] == 0)
            queue.offer(i);
    }
   while ( !queue.isEmpty()){
       Integer preNode = queue.poll();
       numCourses--;                             //计数，保存已经去掉的课程数量。
       for (int[] pre : prerequisites){
           if (pre[1] == preNode){
               inDegrees[pre[0]]--;
               if (inDegrees[pre[0]] == 0)
                   queue.offer(pre[0]);
           }

       }
   }
   return numCourses==0;
}
```

深度优先搜索，如果存在环，那么某次深度优先搜索会访问同一节点两次。

	* 已经被方位的节点标记为-1
 * 本次已经被访问，子节点没有被访问，标记为1
   	* 则在同一次搜索中，若是发现某个节点已经被访问过（标记为1），则发现了环

```Java
public static boolean canFinish(int numCourses, int[][] prerequisites) {
    int flags[] = new int[numCourses];
    for (int i = 0; i < flags.length; i++) {
        flags[i] = 0 ;
    }
    for(int[] p : prerequisites){
        if ( ! dfs(p[1],flags,prerequisites)){
            return false;
        }
    }
    return true;
}

public static boolean dfs(int courseNum,int[] flags,int[][] pre){
    if (flags[courseNum] == -1) return true;
    if (flags[courseNum] == 1) return false;
    flags[courseNum] = 1;

    for(int[] p : pre){
        if (p[1] == courseNum){
            if ( dfs(p[0],flags,pre)== false)
                return false;
        }
    }
    flags[courseNum] = -1;
    return true;
}
```

​	