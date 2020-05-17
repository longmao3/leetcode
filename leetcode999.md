leetcode999

* 要封装啊，对于方向问题，可以使用数组。

```java
class Solution {
    public int numRookCaptures(char[][] board) {
        int m=board.length,n=board[0].length;
        int i=0,j=0,k=0;
        boolean find=false;
        int count = 0;
        for(i=0;i<m;i++){
            for(j=0;j<n;j++){
                if(board[i][j] == 'R') {
                   find=true;
                   break;  
                }      
            }
            if(find) break;
        }
        if(i==m && j==n) return count;
        for(k=i-1;k>=0;k--){
            if(board[k][j] == 'B'){
                break;
            }else if(board[k][j] == 'p'){
                count++;
                break;
            }
        }
        for(k=i+1;k<m;k++){
            if(board[k][j] == 'B'){
                break;
            }else if(board[k][j] == 'p'){
                count++;
                break;
            }
        }
        for(k=j-1;k>=0;k--){
            if(board[i][k] == 'B'){
                break;
            }else if(board[i][k] == 'p'){
                count++;
                break;
            }
        }
        for(k=j+1;k<n;k++){
            if(board[i][k] == 'B'){
                break;
            }else if(board[i][k] == 'p'){
                count++;
                break;
            }
        }
        return count;
    }
}
```

