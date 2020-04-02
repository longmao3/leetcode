[leetcode289](https://leetcode-cn.com/problems/game-of-life/)

解法一：定义复合状态：

* 2：之前是活的，现在是死的；
* -1：之前是死的，现在是活的。

```java
class Solution {
    int m;
    int n;
    public void gameOfLife(int[][] board) {
        int[][] dir = {{-1,-1},{-1,0},{-1,1},
                        {0,-1},{0,1},
                        {1,-1},{1,0},{1,1}};
        m=board.length;
        if(m==0) {
            return;
        }
        n=board[0].length;
        int count;
        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                count = countLiveNeighbors(i,j,dir,board);
                if(board[i][j] == 1){
                    if(count<2 || count>3){
                        board[i][j] = 2;
                    }
                }else if(board[i][j] == 0){
                    if(count == 3){
                        board[i][j] = -1;
                    }
                }
               
            }
        }
        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                if(board[i][j] == 2){
                    board[i][j] = 0;
                }else if(board[i][j] == -1){
                    board[i][j]=1;
                }
                
            }
        }



    }
    public int countLiveNeighbors(int i,int j,int[][] dir,int[][] board){
        int count = 0;
        int tmp_i,tmp_j; //这样的名字很容易搞混淆，要改。
        for(int[] a : dir){
            tmp_i=i+a[0];
            tmp_j=j+a[1];
            if(inAera(tmp_i,tmp_j)){
                if(board[tmp_i][tmp_j]==1 || board[tmp_i][tmp_j]==2){
                    count++;
                }
            }
        }
        return count;
    }
    public boolean inAera(int i,int j){
        if(i>=0 && i<m && j>=0 && j<n){
            return true;
        }
        return false;
    }
}
```

解法二：找到活着的细胞，让他去影响周围的细胞，让周围细胞每个加10；

```java
class Solution {
    int m;
    int n;
    public void gameOfLife(int[][] board) {
        int[][] dir = {{-1,-1},{-1,0},{-1,1},
                        {0,-1},{0,1},
                        {1,-1},{1,0},{1,1}};
        m=board.length;
        if(m==0) {
            return;
        }
        n=board[0].length;
        int count;
        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                if((board[i][j]&1) == 1){  //位运算优先级低于==与，记得使用（）
                    for(int[] a : dir){
                        int col,row;
                        col=i+a[0];
                        row=j+a[1];
                        if(inAera(col,row)){
                           board[col][row]+=10;
                        }
                    }
                }
               
            }
        }
        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                if((board[i][j]&1) == 1 ){
                    if( board[i][j] < 21 || board[i][j] >31){
                         board[i][j] = 0;
                    }else{
                        board[i][j]=1;
                    }
                   
                }else{
                    if(board[i][j] == 30){  //刚好周围三个活的
                        board[i][j] = 1;
                    }else{
                        board[i][j] = 0;
                    }
                }
            }
        }
    }
    public boolean inAera(int i,int j){
        if(i>=0 && i<m && j>=0 && j<n){
            return true;
        }
        return false;
    }
}
```

