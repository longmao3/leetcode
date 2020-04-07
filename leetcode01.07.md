[leetcode01.07](https://leetcode-cn.com/problems/rotate-matrix-lcci/)

* 先沿着对角线翻转，再沿着垂直中线对折。

```java
class Solution {
    public void rotate(int[][] matrix) {
        int len = matrix.length;
        if(len == 0) return;
        for(int r=0;r<len;r++){
            for(int c=r+1;c<len;c++){
                int tmp=matrix[r][c];
                matrix[r][c]=matrix[c][r];
                matrix[c][r]=tmp;
            }
        }

         for(int r=0;r<len;r++){
            for(int c=0;c<len/2;c++){
                int tmp=matrix[r][c];
                matrix[r][c]=matrix[r][len-1-c];
                matrix[r][len-1-c]=tmp;
            }
        }
        return;
    }
}
```

解法二

```java
class Solution {
    public void rotate(int[][] matrix) {
        int len = matrix.length;
        for(int row=0;row<(len+1)/2;row++){
            for(int col=0;col<len/2;col++){
                /*向左旋转了。
                int tmp = matrix[row][col];  
                matrix[row][col]=matrix[col][len-1-row];
                matrix[col][len-1-row]=matrix[len-1-row][len-1-col];
                matrix[len-1-row][len-1-col]=matrix[len-1-col][row];
                matrix[len-1-col][row]=tmp;
                */
                //向右旋转。
                int tmp = matrix[row][col];
                matrix[row][col]=matrix[len-1-col][row];
                matrix[len-1-col][row]=matrix[len-1-row][len-1-col];
                matrix[len-1-row][len-1-col]=matrix[col][len-1-row];
                matrix[col][len-1-row]=tmp;
            }
        }  
        return;   
    }
}
```

