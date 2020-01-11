[leetcode165](https://leetcode-cn.com/problems/compare-version-numbers/submissions/)

`\\.` 第一个\使后面一个\生效。

```java
javapublic static int compareVersion(String version1, String version2) {
    String[] ver_1 = version1.split("\\.");
    String[] ver_2 = version2.split("\\.");
    int len_1 = ver_1.length,len_2=ver_2.length;

    int temp_1;
    int temp_2;
    int minLen= len_1>len_2?len_2:len_1;
    for (int i = 0; i < minLen; i++) {
         temp_1=Integer.parseInt(ver_1[i]);
         temp_2= Integer.parseInt(ver_2[i]);
        if (temp_1>temp_2) return 1;
        else if (temp_1<temp_2) return -1;
    }

    if (len_1 > minLen){
        for (int i = minLen; i < len_1; i++) {
            if (Integer.parseInt(ver_1[i]) != 0)
                return 1;
        }
    }
    if (len_2 > minLen){
        for (int i = minLen; i < len_2; i++) {
            if (Integer.parseInt(ver_2[i]) != 0)
                return -1;
        }
    }
    return 0;
}
```