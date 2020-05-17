leetcode74

* 记住基础的表达，善于利用已经稳定的写法。

  ```java
  while (start <= end){
      mid = start+(end-start)/2; //这样最后start=end 指向刚好小于这个数的一个。
      if (matrix[mid][0] == target)
          return true;
      else if (matrix[mid][0] > target)
          end=mid-1;
      else
          start=mid+1;
  }
  ```

  可以覆盖start和end，

  * 需要返回刚好比target大的`return start`
  * 需要返回刚好比target小的`return end`

  * 注意可能出界。

```java
public static boolean searchMatrix(int[][] matrix, int target) {
    if (matrix.length == 0 || matrix[0].length == 0) return false;
    int start = 0;
    int end = matrix.length-1;
    int mid = 0;
    int row = 0;
    while (start <= end){
        mid = start+(end-start)/2; //这样最后start=end 指向刚好小于这个数的一个。
        if (matrix[mid][0] == target)
            return true;
        else if (matrix[mid][0] > target)
            end=mid-1;
        else
            start=mid+1;
    }

    row = end;
    if (end<0) return false;
    start=0;
    end=matrix[row].length-1;
    while (start<=end){
        mid = start+(end-start+1)/2; //这样最后start=end 指向刚好小于这个数的一个。
        if (matrix[row][mid] == target)
            return true;
        else if (matrix[row][mid] > target)
            end=mid-1;
        else
            start=mid+1;
    }
    return false;
}

public static void main(String[] args) {
    int[][] a = {{1},{3}};
    searchMatrix(a,4);
}
```