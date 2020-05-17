[leetcode80](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array-ii/)

​	

```java
public int removeDuplicates(int[] nums) {
    int pre = 2;
    int index = 2;
    while (index<nums.length){
         if (nums[index] != nums[pre-2]){
             nums[pre] = nums[index];
             pre++;
             index++;
         }else index++;
    }
    return pre;
}
```