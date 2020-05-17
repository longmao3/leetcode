[leetcode394](https://leetcode-cn.com/problems/decode-string/)

解法一：使用栈。

​	将其自内而向外展开。

还需思考。

```java
class Solution {
    public String decodeString(String s) {
        StringBuilder res = new StringBuilder();
        int mutil = 0;
        Stack<Integer> stack_mutil = new Stack<Integer>();
        Stack<StringBuilder> stack_res = new Stack<StringBuilder>();
        for(char c : s.toCharArray()){
            if(c == '['){
                stack_mutil.push(mutil);
                stack_res.push(res);
                mutil = 0;
                res= new StringBuilder();
            }else if(c == ']'){  //弹出一层，即展开了一对[]。
                StringBuilder tmp = new StringBuilder();
                mutil=stack_mutil.pop();
                StringBuilder last_res = stack_res.pop();
                for(int i=0;i<mutil;i++){
                    tmp.append(res);
                }
                mutil=0; //防止刑如"3[a]2[bc]"，产生32
                res = last_res.append(tmp);
            }else if (c>='0' && c<= '9') mutil=mutil*10+c-'0';
            else res.append(c);
        } 
        return res.toString();

    }
} 
```

解法二：

和解法一的思路类似，但是使用了递归的解法。

* 遇到`[`向下递归，遇到`]`本层递归返回，返回后上层递归继续处理剩余部分，如`3[3][a]bc]`的`bc`部分。
* 遇到`]`本层返回。

```java
  public String decodeString(String s) {
        int[] index = {0};
        StringBuilder res = dfs(s,index);
        return res.toString();
    }

    public StringBuilder dfs(String s,int[] index){
        StringBuilder builder = new StringBuilder();
        int mutil=0;
        while(index[0] < s.length()){
            char c = s.charAt(index[0]);
            if(c == '['){
                index[0]++;  //注意本层和递归的下一层之间的联系，每一层改变index【0】使其都指向								 //了‘[’,']'的下一个节点
               StringBuilder tmp = dfs(s,index);  //递归之后可以继续在本层进行处理。
               while(mutil > 0){
                   builder.append(tmp);
                   mutil--;
               }
            }else if(c ==']'){
                index[0]++;
                return builder;
            }else if(c >= '0' && c<='9'){
                mutil=mutil*10+c-'0';
                index[0]++;
            }else{
                builder.append(c);
                index[0]++;
            }
        }
        return builder;
    }
```



​	

