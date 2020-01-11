[leetcode33](https://leetcode-cn.com/problems/search-in-rotated-sorted-array/submissions/)


* 关键在于查找到旋转点。

  * 旋转数组经过二分查找：

    * 如果mid大于起始点，说明旋转点在右侧

    * 如果mid小于起始点，说明旋转点在右侧

  * 经过二分查找，仍然是一个旋转数组结构
**先整理好思路** 
```java 
public static int search(int[] nums, int target) {
    if (nums.length == 0) return -1;
    int start=0,end=nums.length-1;
    int indexOfRotate=nums.length;    //如果没有旋转，直接指向数组最后一个元素的下一个。
    if (nums[end] < nums[start]){ //一定是一个旋转数组
        while (start < end) {
            int mid = start + (end - start+1) / 2; //如果只剩下两个，即start+1=end 防止死循环。
                                                  // 如果是两个，那么一定是end。
            if ( nums[mid] < nums[mid - 1]) {
                indexOfRotate = mid;
                break;
            } else if (nums[mid] > nums[start])
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

public static int binarySearch(int start,int end,int[] nums,int target){
    while (start <= end){
        int mid=start+(end-start)/2;
        if (nums[mid] == target) return mid;
        if (nums[mid]>target)
            end=mid-1;
        else
            start=mid+1;
    }
    return -1;
}
```





```java
public int[] searchRange(int[] nums, int target) {
    int[] ans={-1,-1};
    if (nums == null || nums.length == 0) return ans;
    int left = binarySearchLeft(nums, target );
    int right = binarySearchRight(nums, target);
    if (right < left)
        return ans;
    else {
        ans[0]=left;
        ans[1]=right;
    }
    return ans;
}

public static int binarySearchLeft(int[] nums, int target){
    int start=0,end=nums.length-1;
    while (start <=  end){
        int mid=start+(end-start)/2;
        if (nums[mid] >= target)
            end=mid-1; //将大于等于目标的排除在右侧
        else
            start=mid+1;
    }
    return  end+1; 
}

public static int binarySearchRight(int[] nums, int target){
    int start=0,end=nums.length-1;
    while (start <=  end){
        int mid=start+(end-start)/2;
        if (nums[mid] <= target)
            start=mid+1; //将小于等于的排除在左侧
        else
            end=mid-1;
    }
    return  start-1; 
}
```