[leetcode81](https://leetcode-cn.com/problems/search-in-rotated-sorted-array-ii/submissions/)

同 [leetcode33](https://leetcode-cn.com/problems/search-in-rotated-sorted-array/)

* 12111111出现这种情况，无法判断，旋转点在前半段还是后半段，所以要先去重。

```java 
public static boolean search(int[] nums, int target) {
    if (nums.length == 0) return false;
    int start=0,end=nums.length-1;
    int indexOfRotate=nums.length;      //如果没有旋转，直接指向数组最后一个元素的下一个。
    while (end > 0 && nums[end] == nums[start])  end--;   
    indexOfRotate = end+1;              //如果indexOfRotate没有更新，防止出现类似  1211111的情况，否则二分查找就不行了。
    if (nums[end] < nums[start]){       //一定是一个旋转数组
        while (start < end) {
            int mid = start + (end - start+1) / 2;  //如果只剩下两个，即start+1=end 防止死循环。
            // 如果是两个，那么一定是end。
            if ( nums[mid] < nums[mid - 1]) {
                indexOfRotate = mid;
                break;
            } else if (nums[mid] >= nums[start])
                start = mid;   //不要加一，因为可能破坏旋转数组的结构
            else
                end = mid-1 ;
        }
    }
    if (target >= nums[0])
        return binarySearch(0,indexOfRotate-1,nums,target);
    else
        return binarySearch(indexOfRotate,nums.length-1,nums,target);
}

public static boolean binarySearch(int start,int end,int[] nums,int target){
    while (start <= end){
        int mid=start+(end-start)/2;
        if (nums[mid] == target) return true;
        if (nums[mid]>target)
            end=mid-1;
        else
            start=mid+1;
    }
    return false;
}
```