[leetcode39](https://leetcode-cn.com/problems/combination-sum/submissions/)

做搜索、回溯问题的套路是画图，代码其实就是根据画出的树形图写出来的。

```java
private List<List<Integer>> lists= new ArrayList<>();
private List<Integer> list = new ArrayList<>();

public List<List<Integer>> combinationSum(int[] candidates, int target) {
    combinationSumHelper(0,candidates,target);
    return lists;
}

public void combinationSumHelper(int from,int[] candidates, int target) {
    if (target == 0) {
        lists.add(list);
        list=new ArrayList<>(list);
    }else if (target<0)
        return;
    for (int i = from; i < candidates.length; i++) {
        list.add(candidates[i]);
        combinationSumHelper(i,candidates,target-candidates[i]);
        list.remove(list.size()-1);
    }
}
```

优化

排序对于去重没有作用，只是使循环次数变少了。

```Java
private List<List<Integer>> lists= new ArrayList<>();
private List<Integer> list = new ArrayList<>();

public List<List<Integer>> combinationSum(int[] candidates, int target) {
    Arrays.sort(candidates); //排序后相邻数字更为接近，可以提前退出，达到剪枝效果。
    combinationSumHelper(0,candidates,target);
    return lists;
}

public void combinationSumHelper(int from,int[] candidates, int target) {
    if (target == 0) {
        lists.add(list);
        list=new ArrayList<>(list);
    }else if (target<0)
        return;
    for (int i = from; i < candidates.length; i++) {
        list.add(candidates[i]);
        combinationSumHelper(i,candidates,target-candidates[i]);
        list.remove(list.size()-1);
    }
}
```

