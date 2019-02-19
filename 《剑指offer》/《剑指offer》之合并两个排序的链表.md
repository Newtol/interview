# 《剑指offer》之合并两个排序的链表

题目：输入两个单调递增的链表，输出两个链表合成后的链表，当然我们需要合成后的链表满足单调不减规则。

分析：要实现两个已经排序好的链表的合并，其实就是需要逐一比较链表中的值，然后进行合并。同时需要注意两个列表为空的情况。思路如图所示：

![](https://github.com/Newtol/interview/blob/master/Img/%E5%90%88%E5%B9%B6%E4%B8%A4%E4%B8%AA%E9%93%BE%E8%A1%A8.png)

解决方案：

+ 非递归实现：

  代码：

  ```java
  public ListNode Merge(ListNode list1,ListNode list2) {
      // 防止list1和list2为空的情况
      if(list1 == null){
          return list2;
      }
      if(list2 == null){
          return list1;
      }
      // 新的链表
      ListNode result = null;
      // 新的链表的指针
      ListNode current = null;
      while(list1!=null && list2!=null){
          if(list1.val <= list2.val){
              // 第一次遍历头结点为空时
              if(result == null){
                  result = current = list1;
              }else{
                  // 将较小值追加至新的链表的尾部
                  current.next = list1;
                  // 向后移动指针
                  current = list1;
              }
              list1 = list1.next;
          }else{
              if(result == null){
                  result = current = list2;
              }else{
                  current.next = list2;
                  current = list2;
              }
              list2 = list2.next;
          }
      }
      // 当list1和list2不等长时，直接将对于部分追加至链表尾部
      if(list1 == null){
          current.next = list2;
      }else{
          current.next = list1;
      }
      return result;
  }
  ```

  测试性能分析：

  ```java
  运行时间：22ms
  占用内存：9272k
  ```

+ 递归实现：

  代码：

  ```java
  public ListNode Merge(ListNode list1,ListNode list2) {
      if(list1 == null){
          return list2;
      }
      if(list2 == null){
          return list1;
      }
      ListNode listNode;
      if(list1.val<list2.val){
          listNode = list1;
          listNode.next = Merge(list1.next,list2);
      }else{
          listNode = list2;
          listNode.next = Merge(list1,list2.next);
      }
      return listNode;
  }
  ```

  测试性能分析：

  ```
  运行时间：32ms
  占用内存：9508k
  ```
