[leetcode542](https://leetcode-cn.com/problems/01-matrix/)

* 采用深度优先搜索，其实自己没有想到这个解法是自己没有想到如何处理“多源点”的方法。

```java
class Solution {
    public int[][] updateMatrix(int[][] matrix) {
        int n = matrix.length;
        int m = matrix[0].length;
        int [][] res = new int[n][m];
        boolean [][] visited = new boolean[n][m];
        Queue<Integer[]> queue = new LinkedList<>();
        for(int i=0;i<n;i++){
            for(int j=0;j<m;j++){
                if(matrix[i][j]== 0){
                    queue.offer(new Integer[]{i,j});
                    visited[i][j] = true;
                }
            }
        }
        int count = 0;
        int[][] dirs = {{-1,0},{1,0},{0,1},{0,-1}};
        while(!queue.isEmpty()){
            int size = queue.size();
            for(int i=0;i<size;i++){
                Integer[] a = queue.poll();
                res[a[0]][a[1]] = count;
                for(int[] dir:dirs){
                    int newX=a[0]+dir[0];
                    int newY=a[1]+dir[1];
                    if(newX>=0 && newX<n && newY>=0 && newY<m && visited[newX][newY] == false){
                        queue.offer(new Integer[]{newX,newY});
                        visited[newX][newY] = true;
                    }
                }

            }
            count++;
        }
        return res;

    }
}
```

