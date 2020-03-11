[leetcode417](https://leetcode-cn.com/problems/pacific-atlantic-water-flow/)

* 逆向思维。
* 要是思路有点困难，就使用增加存储空间。

```java
class Solution {
    int m,n;
    public List<List<Integer>> pacificAtlantic(int[][] matrix) {
        List<List<Integer>> ans = new ArrayList<>();
        m = matrix.length;
        if(m == 0) return ans;
        n = matrix[0].length;
        int[][] pa = new int[m][n];
        int[][] at = new int[m][n];
        for(int i=0;i<m;i++){
            dfs(i,0,pa,matrix);
            dfs(i,n-1,at,matrix);
        }
        for(int i=0;i<n;i++){
            dfs(0,i,pa,matrix);
            dfs(m-1,i,at,matrix);
        }
        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                if(pa[i][j] == 1 && at[i][j] == 1){
                    ArrayList tmp = new ArrayList();
                    tmp.add(i);
                    tmp.add(j);
                    ans.add(tmp);
                }
            }
        }
        return ans;
    }
    public boolean inArea(int x,int y){
        if(x>=0 && x<m && y>=0 && y<n) 
            return true;
        else
            return false;
    }

    public void dfs(int x,int y,int[][] ocean,int[][] matrix){
        if(ocean[x][y] == 1) return;
        ocean[x][y] = 1;
        int[][] dir = {{-1,0},{1,0},{0,-1},{0,1}};
        for(int[] a : dir){
            int new_x=x+a[0];
            int new_y=y+a[1];
            if(inArea(new_x,new_y) && matrix[new_x][new_y] >= matrix[x][y])
                dfs(new_x,new_y,ocean,matrix);
        }
    }
}
```

