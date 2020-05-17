[leetcode75](https://leetcode-cn.com/problems/sort-colors/)

​	

```java
public void sortColors_1(int[] nums) {
    int p0 = 0, cur = 0, p2 = nums.length - 1;
    int tmp = 0;
    while (cur <= p2) {
        switch (nums[cur]) {
            case 0:
                tmp = nums[p0];   //必须采用交换，防止p0==cur
                nums[p0] = nums[cur];
                nums[cur] = tmp;
                p0++;
                cur++;
                break;
            case 1:
                cur++;
                break;
            case 2:
                nums[cur] = nums[p2];
                nums[p2] = 2;
                p2--;
                break;
        }
    }
}

public void sortColors(int[] nums) {
    int p0 = 0, cur = 0, p2 = nums.length - 1;
    int tmp = 0;
    while (cur <= p2) {
        if (nums[cur] == 0) {
            tmp = nums[p0];  //必须采用交换，防止p0==cur
            nums[p0] = nums[cur];
            nums[cur] = tmp;
            p0++;
            cur++;

        }else if (nums[cur] == 1) cur++;
        else {
            nums[cur] = nums[p2];
            nums[p2] = 2;
            p2--;
        }
    }
}
```

