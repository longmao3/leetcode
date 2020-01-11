[leetcode6](https://leetcode-cn.com/problems/zigzag-conversion/solution/shun-xu-fang-wen-zi-fu-chuan-by-ypzro5mtzw/)

```java
public String convert(String s, int numRows) {
    if (numRows == 1) return s;
    StringBuilder[] builders=new StringBuilder[numRows];
    for (int i = 0; i < builders.length; i++) {
        builders[i] = new StringBuilder();
    }
    int index=1;
    builders[0].append(s.charAt(0));
    boolean flag=true;
    for (int i = 1; i < s.length(); i++) {
        builders[index].append(s.charAt(i));
      /*
        if (curRow == 0 || curRow == numRows - 1) goingDown = !goingDown;
        curRow += goingDown ? 1 : -1;
    */

        if (flag) index++;
        else index--;
        if (index>=numRows){
            index=index-2;
            flag=false;
        }else if (index<=-1){
            index=1;
            flag=true;
        }
 }
    for (int i = 1; i < builders.length; i++) {
        builders[0].append(builders[i]);
    }
    return builders[0].toString();
}
```