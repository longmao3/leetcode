[leetcode43](https://leetcode-cn.com/problems/multiply-strings/submissions/)

​	

```java
public static String multiply(String num1, String num2) {
    String ans = new String();
    for (int i = 0; i < num2.length(); i++) {
        if (! ans.equals("0")) ans+='0';
        String mul = multiply(num1, num2.charAt(i));
        ans=addStrings(ans,mul);
    }
    return ans;
}
public static String multiply(String num1,char c){
    if (c == '0') return "0";
    StringBuilder builder= new StringBuilder();
    int carry=0;
    for (int i = num1.length()-1; i >=0 ; i--) {
        int tmp=(num1.charAt(i)-'0')*(c-'0');
        tmp+=carry;
        builder.append(tmp%10);
        carry=tmp/10;
    }
    if (carry != 0) builder.append(carry);
    return builder.reverse().toString();
}

public static String addStrings(String num1, String num2) {
    int length_1=num1.length(),length_2=num2.length();
    int minLenth=length_1>length_2?length_2:length_1;
    StringBuilder builder = new StringBuilder();
    int flag=0;
    for (int i = 0; i < minLenth; i++) {
        char temp=(char)(num1.charAt(length_1-1-i)-'0'+num2.charAt(length_2-1-i)+flag); //只减去一个’0‘
        if (temp > '9'){
            flag=1;
            temp-=10;
        }else flag=0;
        builder.append(temp);
    }
    for (int i = minLenth; i < length_1; i++) {
        char temp=(char)(num1.charAt(length_1-1-i)+flag);
        if (temp > '9'){
            flag=1;
            temp-=10;
        }else flag=0;
        builder.append(temp);
    }
    for (int i = minLenth; i < length_2; i++) {
        char temp=(char)(num2.charAt(length_2-1-i)+flag); //只减去一个’0‘
        if (temp > '9'){
            flag=1;
            temp-=10;
        }else flag=0;
        builder.append(temp);
    }
    if (flag == 1) builder.append('1');
    return builder.reverse().toString();
}
```

