[leetcode415](https://leetcode-cn.com/problems/add-strings/solution/stringbuilderfan-zhuan-by-ypzro5mtzw/)



```java
public String addStrings(String num1, String num2) {
    int length_1=num1.length(),length_2=num2.length();
    int minLenth=length_1>length_2?length_2:length_1;
    StringBuilder builder = new StringBuilder();
    int flag=0;
    for (int i = 0; i < minLenth; i++) {   //i 代表倒数第几个
        char temp=(char)(num1.charAt(length_1-1-i)-'0'+num2.charAt(length_2-1-i)+flag); //只减去一个’0‘
        if (temp > '9'){
            flag=1;
            temp-=10; //减掉多余的
        }else flag=0;
        builder.append(temp);
    }
    for (int i = minLenth; i < length_1; i++) {  //有可能连续进位。
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