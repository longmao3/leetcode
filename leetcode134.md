[leetcode134](https://leetcode-cn.com/problems/gas-station/)

[参考](https://leetcode-cn.com/problems/gas-station/solution/jia-you-zhan-by-leetcode/)

```java
class Solution {
    public int canCompleteCircuit(int[] gas, int[] cost) {
        int n = gas.length;
        int total_gas = 0;
        int start_position = 0;
        int  tank_gas = 0;
        for(int i = 0;i<n;i++){
            tank_gas+=gas[i]-cost[i];
            total_gas+=gas[i]-cost[i];
            if(tank_gas < 0){
                start_position=i+1;
                tank_gas = 0;
            } 
        }
        return total_gas>=0?start_position:-1;
    }
}
```

[参考](https://leetcode-cn.com/problems/gas-station/solution/shi-yong-tu-de-si-xiang-fen-xi-gai-wen-ti-by-cyayc/)

```java
 public int canCompleteCircuit(int[] gas, int[] cost) {
        int n = gas.length;
        int spare = 0;
        int minSpare = Integer.MAX_VALUE;
        int minIndex = 0;
        for(int i=0;i<n;i++){
            spare+=gas[i]-cost[i];
            if(spare < minSpare){
                minIndex = i;
                minSpare = spare;
            }
        }
        return spare >=0?(minIndex+1)%n:-1;
    }
```

