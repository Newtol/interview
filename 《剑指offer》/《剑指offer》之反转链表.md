# 《剑指offer》之反转链表

题目：输入一个链表，反转链表后，输出新链表的表头

分析：实现链表的反转，需要连续三个节点(A,B,C)之间的配合。即: C节点指向B节点，然后B节点指向A节点。然后整体再向后移动一个节点，重复操作，即可实现链表的反转。

+ 代码：

  ```java
   public ListNode ReverseList(ListNode head) {
       // 上一节点
       ListNode reverhead = null;
       // 下一节点
       ListNode next = null;
       // 当前节点
       ListNode current =head;
       // 判断是否遍历完成
       while (current!= null) {
           // 保存分析中的节点C
           next = current.next;
           // B节点指向上一节点A
           current.next =  reverhead;
           // 整体节点向后移动
           reverhead = current;
           current = next;
       }
       return  reverhead;
   }
  ```

  测试性能分析：

  ```
  运行时间：21ms
  占用内存：9596k
  ```
