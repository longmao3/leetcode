[leetcode304](https://leetcode-cn.com/problems/range-sum-query-2d-immutable/solution/dp-by-ypzro5mtzw-5/)

​	dp求解 

* `sumMatrix[i][j]`代表以i行j列为右下角的矩形内所有元素的和。

```java
public class NumMatrix {
        int[][] sumMatrix;


        public NumMatrix(int[][] matrix) {
            int n=matrix.length;
            if (n==0) return;
            int m=matrix[0].length;
            sumMatrix=new int[n+1][m+1];
            for (int i = 1; i < n+1; i++) {
                for (int j = 1; j < m+1; j++) {
                    sumMatrix[i][j]=matrix[i-1][j-1]+sumMatrix[i-1][j]
                            +sumMatrix[i][j-1]-sumMatrix[i-1][j-1];
                }
            }
        }

        public int sumRegion(int row1, int col1, int row2, int col2) {
             return  sumMatrix[row2+1][col2+1]-sumMatrix[row1][col2+1]
                        -sumMatrix[row2+1][col1]+sumMatrix[row1][col1];
        }

}
```