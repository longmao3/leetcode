[leetcode151](https://leetcode-cn.com/problems/reverse-words-in-a-string/)

* 特殊输入判断
* 能用API就用API。

```java
class Solution {
    public String reverseWords(String s) {
        if(s == null || s.trim().equals("")) return s.trim();
        char[] chars = s.trim().toCharArray();
        int start,count=0; //重复空格计数
        for(int i=0;i<chars.length;i++){ //外层循环不复制空格，只有内层循环复制最后一个空格。
            if(chars[i] != ' '){
                chars[i-count] = chars[i];
                start=i-count;
                for(;i<chars.length;i++){
                    chars[i-count]=chars[i];
                    if(chars[i] == ' '){
                        reverse(chars,start,i-1-count);
                        break;
                    }else if(i == chars.length-1){
                        reverse(chars,start,i-count);
                    }
                }
            }else if(i>0 && chars[i-1] == ' '){
                count++;
            }         
        }
        reverse(chars,0,chars.length-1-count);
        String ans = new String(chars);
        return ans.substring(0,ans.length()-count);
    }
    public void reverse(char[] chars,int start,int end){
        for(int i=start,j=end;i<=start+(end-start)/2;i++,j--){ //取几个特例判断一下。
            char tmp = chars[i];
            chars[i] = chars[j];
            chars[j] = tmp;
        }
    }
}
```

懒人做法

```java
public String reverseWords(String s) {
    String[] split = s.split(" ");
    StringBuilder builder = new StringBuilder();
    for (int i = split.length-1; i >=0 ; i--) {
        if (split[i].equals("")) continue;
        if (i == split.length-1) builder.append(split[i]);
        else builder.append(" "+split[i]);
    }
    return builder.toString();
}
```

