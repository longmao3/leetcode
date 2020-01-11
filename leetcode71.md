[leetcode71](https://leetcode-cn.com/problems/simplify-path/)	

```java 
public String simplifyPath(String path) {
    Stack<String> s = new Stack<>();
    String[] split = path.split("/");
    for (int i = 0; i < split.length; i++) {

        /*
            else if (!s[i].equals("") && !s[i].equals(".") && !s[i].equals(".."))
            stack.push(s[i]);
            把需要处理的处理一下，其他忽略就行。
         */
        if (split[i].equals("..") && !s.isEmpty()){
            s.pop();
            continue;
        }else if (split[i].equals("..") ){
            continue;
        }
        if (split[i].equals(".") || split[i].equals("")) continue;
        s.push(split[i]);
    }

    if (s.isEmpty()) return "/";
    StringBuilder builder = new StringBuilder();
    for (int i = 0; i <s.size(); i++) {
        builder.append("/"+s.get(i));
    }
    return builder.toString();
}
```