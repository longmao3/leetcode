[leetcode73](https://leetcode-cn.com/problems/set-matrix-zeroes/submissions/)

[参考](https://leetcode-cn.com/problems/set-matrix-zeroes/solution/ju-zhen-zhi-ling-by-leetcode/)

* 在原数组标记某行某列是否应该被置为零。

```java
public void setZeroes(int[][] matrix) {
    boolean isCol = false;
    for (int i = 0; i < matrix.length; i++) {
        for (int j = 0; j < matrix[0].length; j++) {
            if (matrix[i][j] == 0){
                matrix[i][0] = 0;
                if (j != 0)
                    matrix[0][j] = 0;
                else 
                    isCol = true;
            }
        }
    }

    for (int i = 1; i < matrix.length; i++) {
        for (int j = 1; j < matrix[0].length; j++) {
            if (matrix[i][0] == 0 || matrix[0][j] == 0)
                matrix[i][j]=0;
        }
    }
    if (matrix[0][0] == 0)
        for (int i = 0; i < matrix[0].length; i++) {
            matrix[0][i]=0;
        }
    if (isCol)
        for (int i = 0; i < matrix.length; i++) {
            matrix[i][0] = 0;
        }
}
```