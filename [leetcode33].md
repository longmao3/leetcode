[leetcode33](https://leetcode-cn.com/problems/search-in-rotated-sorted-array/submissions/)


* 关键在于查找到旋转点。

  * 旋转数组经过二分查找：

    * 如果mid大于起始点，说明旋转点在右侧

    * 如果mid小于起始点，说明旋转点在右侧
* 经过二分查找，仍然是一个旋转数组结构
* **先整理好思路**（注意归一条件，简化编程）
* 对于二分法直接从只剩两个点开始分析，或者三个点吧。

```java 
public static int search(int[] nums, int target) {
    if (nums.length == 0) return -1;
    int start=0,end=nums.length-1;
    int indexOfRotate=nums.length;    //如果没有旋转，直接指向数组最后一个元素的下一个。
    if (nums[end] < nums[start]){ //一定是一个旋转数组
        while (start < end) {
            int mid = start + (end - start+1) / 2; //如果只剩下两个，即start+1=end 防止死循环。
                                                  // 如果是两个，那么一定是end。
            									  //这个操作保证，只剩下两个时指向后一个，end-start=偶数时，指向后一个。
            if ( nums[mid] < nums[mid - 1]) {
                indexOfRotate = mid;
                break;
            } else if (nums[mid] > nums[start])
                start = mid;   //不要加一，因为可能破坏旋转数组的结构，破坏了这一结构就不能再使用这个算//法了。
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


