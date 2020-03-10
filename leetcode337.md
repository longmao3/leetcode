[leetcode337](https://leetcode-cn.com/problems/house-robber-iii/)

解法一：动态规划+递归

* 若偷当前节点，那么总钱数为 以四个孙子几点为根能偷到的最大钱数之和。
* 若不偷当前节点，那么总钱数为以两个儿子节点为根能偷到的最大钱数之和。

```java
class Solution {
    public int rob(TreeNode root) {
       return helper(root);
    }

    public int  helper(TreeNode node ){
        if(node == null) return 0;
        int money1=0,money2=0;
        money1=helper(node.left)+helper(node.right);
        if(node.left != null){
            money2+=helper(node.left.left)+helper(node.left.right);//注意此处，写成了两个																		//left.right
        }
        if(node.right != null){
            money2+=helper(node.right.left)+helper(node.right.right);
        }
        return Math.max(node.val+money2,money1);
    }
}
```

解法二：在解法一的基础上，改进算法

1. 创建HelpNode，保存了每次搜索的结果，保证了子问题只被计算一次。
2. 算法步骤
   * 构造一个由HelpNode为节点的和原始树结构相同的树。
   * 在新树中进行递归计算如果以当前节点为根则可以偷多少钱，并保存结果防止重复计算。

```java
class Solution {
    public int rob(TreeNode root) {
       if(root == null) return 0;
       HelpeNode newRoot = new HelpeNode(root);
       copyTree(root,newRoot);
       return helper(newRoot);
    }

    public int  helper(HelpeNode node ){
        if(node == null) return 0;
        if(node.flag) return node.robCount;
        if(node.left == null || node.right == null){
            node.robCount = node.innerNode.val;
            node.flag = true;
        }
        int money1=0,money2=0;
        money1=helper(node.left)+helper(node.right);
        if(node.left != null){
            money2+=helper(node.left.left)+helper(node.left.right);
        }
        if(node.right != null){
            money2+=helper(node.right.left)+helper(node.right.right);
        }
        node.robCount =  Math.max(node.innerNode.val+money2,money1);
        node.flag = true;
        return node.robCount;
    }

    public void copyTree(TreeNode root1,HelpeNode root2){
        if (root1.left != null) {
            HelpeNode newNode = new HelpeNode(root1.left);
            root2.left = newNode;
            copyTree(root1.left,root2.left);
        }
        if (root1.right != null){
            HelpeNode newNode = new HelpeNode(root1.right);
            root2.right = newNode;
            copyTree(root1.right,root2.right);
        }
    }

    public static class HelpeNode{
        public TreeNode innerNode;
        public HelpeNode left;
        public HelpeNode right;
        public boolean flag = false;
        public int robCount=0;

        public HelpeNode(TreeNode node){
            this.innerNode=node;
        }
    }
```

解法三：

[参考](https://leetcode-cn.com/problems/house-robber-iii/solution/san-chong-fang-fa-jie-jue-shu-xing-dong-tai-gui-hu/)

对于每个节点，用一个数组，int[0]表是不偷当前节点，int[1]表示偷当前节点。

每个节点可选择偷或者不偷两种状态，根据题目意思，相连节点不能一起偷

* 当前节点选择偷时，那么两个孩子节点就不能选择偷了
* 当前节点选择不偷时，两个孩子节点只需要拿最多的钱出来就行(**两个孩子节点偷不偷没关系**)

总结：这样做的好处是，一个节点只与和它相邻的节点的信息有关，就不会造成解法一那样的同一子问题求解两遍的问题了。

```java 
 public int rob(TreeNode root) {
        int[] rob = robHelper(root);
        return Math.max(rob[0],rob[1]);
    }

    public int[] robHelper(TreeNode root){
        int[] rop = new int[2];
        if(root == null) return rop;

        int[] left = robHelper(root.left);
        int[] right = robHelper(root.right);

        rop[0] = Math.max(left[0],left[1])+Math.max(right[0],right[1]);
        rop[1] = root.val+left[0]+right[0] ;

        return rop;
    }
```