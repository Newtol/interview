# 《剑指offer》之判断是否为子树

题目：输入两棵二叉树A，B，判断B是不是A的子结构。（ps：我们约定空树不是任意一个树的子结构）

分析：在确保两棵树均不为空树的情况下，可根据递归遍历左子树和右子树的方式来实现匹配。一旦树B被遍历完成，无论树A是否被遍历完，都代表匹配成功，否则匹配失败。

解决方案：

+ 递归实现

  代码：

  ```java
  public boolean HasSubtree(TreeNode root1,TreeNode root2) {
      boolean result = false;
      if(root1 != null && root2 != null){
          // 判断根节点是否相同
          if(root1.val == root2.val){
              result = DoesTree1HaveTree2(root1,root2);
          }
          // 判断树A左子树是否与树B根节点相同
          if(!result){
              result = HasSubtree(root1.left, root2);
          }
          // 判断树A右子树是否与树B根节点相同
          if(!result){
              result = HasSubtree(root1.right, root2);
          }
      }
      return result;
  }
  
  public boolean DoesTree1HaveTree2(TreeNode root1,TreeNode root2){
      // 代表树A已经遍历完，但是树B仍有节点，故不匹配
      if(root1 == null && root2 != null) {
          return false;
      }
      // 代表树B已经遍历完成，所以匹配
      if(root2 == null){
          return true;
      }
      // 判断两个节点是否相同
      if(root1.val != root2.val){
          return false;
      }
      //当根节点相同时，判断左右子树是否分别相等
      return DoesTree1HaveTree2(root1.left, root2.left) && DoesTree1HaveTree2(root1.right, root2.right);
  }
  ```

  性能测试分析：

  ```
  运行时间：18ms
  占用内存：9352k
  ```
