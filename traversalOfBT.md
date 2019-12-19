# 二叉树的遍历

[参考](https://qinnsang.github.io/2019/09/12/%E6%A0%91%E7%9A%84%E5%89%8D%E4%B8%AD%E5%90%8E%E5%BA%8F%E5%B1%82%E6%AC%A1%E9%81%8D%E5%8E%86%EF%BC%88%E9%80%92%E5%BD%92%E3%80%81%E8%BF%AD%E4%BB%A3%E3%80%81%E8%8E%AB%E9%87%8C%E6%96%AF%E7%AE%97%E6%B3%95%EF%BC%89/)

# 前序遍历
### 递归：
### 莫里斯遍历 



# 中序遍历
### 递归：
### 莫里斯遍历：

1. 如果左子节点为空:
   * 输出当前节点;
   * 指向右子节点。
2. 否则，找到左子树最右边的节点predecessor,predecessor.right=cur,并断开cur与左子树的连接，然后进入左子树。
     **注意：破坏了二叉树的原本结构。**

```java
	class BSTIterator {
    List<Integer> list=new ArrayList<>();
    int index = 0;//访问下标
    public BSTIterator(TreeNode root) {
        TreeNode cur = root;
        TreeNode predecessor,temp;
        while (cur != null){
            if (cur.left == null){
                list.add(cur.val);
                cur=cur.right;
            }else {
                predecessor = cur.left;
                while (predecessor.right != null) predecessor =predecessor.right;
                predecessor.right = cur;

                temp=cur;
                cur=cur.left;
                temp.left=null; //断开原有连接，防止死循环
            }
        }
    }

    /** @return the next smallest number */
    public int next() {
        return list.get(index++);
    }

    /** @return whether we have a next smallest number */
    public boolean hasNext() {
        return index < list.size();
    }
	}
```

# 后续遍历
### 递归：前序遍历  root->左->右，若将前序遍历改为 root->右节点->左，倒序输出即可。
```java
 public List<Integer> postorderTraversal(TreeNode root) {
        Stack<TreeNode> s = new Stack<>();
        List<Integer> res = new LinkedList<>();
        if (root == null) return res;
        s.push(root);
        while (!s.isEmpty()){
            TreeNode node = s.pop();
            res.add(0,node.val);
            if (node.left != null) s.push(node.left);
            if (node.right != null) s.push(node.right);
        }
        return res;
    }	
```






### 莫里斯遍历
通过建立的临时边，可以让cur返回上层节点，不可避免第第二次沿着相同的路径进行查找，最后删除临时节点。
[参考](https://leetcode-cn.com/problems/binary-tree-preorder-traversal/solution/er-cha-shu-de-qian-xu-bian-li-by-leetcode/)

	 public List<Integer> postorderTraversal(TreeNode root) {
	    List<Integer> res = new LinkedList<>();
	    TreeNode cur = root;
	    TreeNode predecessor;
	    while (cur != null){
	        if (cur.right != null){
	            predecessor = cur.right;
	            while (predecessor.left != null && predecessor.left != cur)
	                predecessor=predecessor.left;
	            if (predecessor.left == null){ //第一次查找到
	                res.add(0,cur.val);
	                predecessor.left = cur; //建立临时连接
	                cur = cur.right;  //进入右子树
	            }else {
	                predecessor.left = null; //断开临时连接，说明右子树已经处理完毕。
	                cur=cur.left; 			//进入左子树
	            }
	        }else {
	            res.add(0,cur.val);
	            cur = cur.left;
	        }
	    }
	    return res;
	}

## 层次遍历

	 public List<Integer> rightSideView_1(TreeNode root) {
	    Queue<TreeNode> q = new LinkedList<>();
	    List<Integer> res = new ArrayList<>();
	    if (root == null) return res;
	    q.offer(root);
	    TreeNode node = null;
	    while ( !q.isEmpty()){
	        int size = q.size();
	        for (int i = 0; i < size; i++) {
	            node = q.poll();
	            if (node.left != null) q.offer(node.left);
	            if (node.right != null) q.offer(node.right);
	        }
	        res.add(node.val);
	    }
	    return res;
	 }

