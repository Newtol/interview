# 《剑指offer》之重构二叉树

题目：输入某二叉树的前序遍历和中序遍历的结果，请重建出该二叉树。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。例如输入前序遍历序列{1,2,4,7,3,5,6,8}和中序遍历序列{4,7,2,1,5,3,8,6}，则重建二叉树并返回。

分析：两种遍历的区别为：

前序遍历：根结点 ---> 左子树 ---> 右子树

中序遍历：左子树---> 根结点 ---> 右子树

解决方案：

+ 我们可以根据前序遍历得到根节点，然后再在中序遍历中找到该节点的左子树和右子树。然后利用递归的思想，将左子树和右子树又分别进行重构，从而实现整个二叉树的重构。

  代码：

  ```java
  public TreeNode reConstructBinaryTree(int [] pre,int [] in) {
          return reConstructBinaryTree(pre,0,pre.length-1,in,0,in.length-1);
      }
  private TreeNode reConstructBinaryTree(int [] pre,int startPre,int endPre,int [] in,int startIn,int endIn) {
  
      if(startPre>endPre||startIn>endIn){
          return null;
      }
      TreeNode root=new TreeNode(pre[startPre]);
  
      for(int i=startIn;i<=endIn;i++){
          if(in[i]==pre[startPre]){
              root.left=reConstructBinaryTree(pre,startPre+1,startPre+(i-startIn),in,startIn,i-1);
              root.right=reConstructBinaryTree(pre,startPre+(i-startIn)+1,endPre,in,i+1,endIn);
              break;
          }
      }
  
      return root;
  }
  ```

+ 测试性能分析

```
运行时间：262ms
占用内存：22756k
```



