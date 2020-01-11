[leetcode31](https://leetcode-cn.com/problems/next-permutation/)

* 全排列要变得稍微大一点，所以要从低位开始变化
  * 首先要找到能变大的位，即从右向左第一降序位i。
  * 又不能变得太大，即找到`nums[i]`右侧刚好大于它的数字，交换。
  * `nums[i] `右侧任然保持升序。
  * 让`nums[i]`右侧翻转以使这部分变得最小。

```java
public void nextPermutation(int[] nums) {
    int i = nums.length-2;
    while (i>=0 && nums[i]>=nums[i+1]){
        i--;
    }
    if (i < 0) {  // 已经成为最大序了。
        reverse(0,nums.length-1,nums);
        return;
    }
    int j=0;
    for ( j = nums.length-1; j > i ; j--) {
        if (nums[j] > nums[i]) 
            break;
    }
    swap(i,j,nums);
    reverse(i+1,nums.length-1,nums);
    return;
}

public void reverse(int start,int end,int[] nums){
   while (start<end){
       int temp = nums[start];
       nums[start] = nums[end];
       nums[end] = temp;
       start++;
       end--;
   }
}

public void swap(int from,int to,int[] nums){
    int temp=nums[from];
    nums[from] = nums[to];
    nums[to] = temp;
}
```

