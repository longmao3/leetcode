[leetcode434](https://leetcode-cn.com/problems/number-of-segments-in-a-string/solution/zhu-yi-pan-kong-by-ypzro5mtzw/)

​	

```java
public int countSegments(String s) {
    if (s.trim().equals("")) return 0;  //注意判空
    int count=0;
    String[] sl = s.split(" ");
    for (int i = 0; i < sl.length; i++) {
        if ( ! sl[i].trim().equals(""))
            count++;
    }
    return count;
}
```