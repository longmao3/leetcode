[leetcode79](https://leetcode-cn.com/problems/word-search/solution/zai-er-wei-ping-mian-shang-shi-yong-hui-su-fa-pyth/)

* 深度优先，找到才返回，找不到继续。



```java
public class Solution {

    boolean[][] isMark;
    int[][] direction;

    public boolean exist(char[][] board, String word) {
        int m = board.length;
        if (m == 0) return false;
        int n = board[0].length;
        isMark = new boolean[m][n];
        int[][] direction = {{-1,0},{1,0},{0,-1},{0,1}};
        this.direction = direction;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (board[i][j] == word.charAt(0)) {
                    isMark[i][j] = true;
                    if( dfs(board, m, n, word, 1, i, j))
                        return true;
                    isMark[i][j] = false;
                }
            }
        }
        return false;
    }

    public boolean dfs(char[][] board,int m,int n,String word,int index,int i,int j){
        if (index >= word.length())  return true;
        for (int k = 0; k <4; k++) {
            int newI = i + direction[k][0];
            int newJ = j + direction[k][1];
            if (check(m,n,newI,newJ) && !isMark[newI][newJ] && board[newI][newJ] == word.charAt(index)){
                isMark[newI][newJ] = true;
                if( dfs(board,m,n,word,index+1,newI,newJ) )
                    return true;
                isMark[newI][newJ] = false;
            }
        }
        return false;
    }

    public boolean check(int m,int n,int i,int j){
        return (i<m && i>=0 && j<n && j>=0);
    }
```

修改：

```java
boolean[][] isMark;
int[][] direction = {{-1,0},{1,0},{0,-1},{0,1}};
int m ;
int n ;
char[] chars;

public boolean exist(char[][] board, String word) {
    this.m = board.length;
    if (m == 0) return false;
    this.n = board[0].length;
    isMark = new boolean[m][n];
    chars=word.toCharArray();
    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            if( dfs(board,0, i, j))
                return true;
        }
    }
    return false;
}

public boolean dfs(char[][] board,int index,int i,int j){
    if (index >= chars.length)  return true;
    if (check(m,n,i,j) && !isMark[i][j] && board[i][j] == chars[index]) {
        isMark[i][j] = true;
        for (int k = 0; k < 4; k++) {
            int newI = i + direction[k][0];
            int newJ = j + direction[k][1];
            if (dfs(board, index + 1, newI, newJ)) //此处需要注意，只有找到才返回。
                return true;
        }
        isMark[i][j] = false;
    }
    return false;
}

public boolean check(int m,int n,int i,int j){
    return (i<m && i>=0 && j<n && j>=0);
}
```

