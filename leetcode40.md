[leetcode40](https://leetcode-cn.com/problems/combination-sum-ii/submissions/)



	* 及时进行剪枝
	* 同一层次的数字不要重复，就可以避免整体重复。
	* 注重画图理解思路。

```java 
private List<List<Integer>> lists= new ArrayList<>();
private List<Integer> list = new ArrayList<>();

public List<List<Integer>> combinationSum2(int[] candidates, int target) {
    if (candidates.length == 0) return lists;
    Arrays.sort(candidates);
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
        if (target-candidates[i] < 0)
            break;  //剪枝，比这个数大的就没有必要再进行遍历了。
        if (i>from && candidates[i-1]==candidates[i])
            continue;    //同一层次不要重复。

        list.add(candidates[i]);
        combinationSumHelper(i+1,candidates,target-candidates[i]);
        list.remove(list.size()-1);
    }
}
```