# 《剑指offer》之链表中倒数第k个结点

题目：输入一个链表，输出该链表中倒数第k个结点。

分析：倒数第k个节点，也就是正数的第n-k+1个节点(链长为n),例如：在n=6的链表中，倒数第2个节点就是正数第5个节点（6-2=1）。

解决方案：

+ 直接遍历法：先遍历一遍链表获得链表长n，然后再从头开始遍历第n-k+1个节点。

  代码：

  ```java
  public ListNode FindKthToTail(ListNode head,int k) {
      ListNode pre = head;
      ListNode last =head;
      int count = 0;
      if(head == null || k <= 0){
          return null;
      }
      while(pre  != null){                     
          pre = pre.next;
          count++;
      }
      if(k>count){
          return null;
      }
      for(int i =1;i<count-k+1;i++){
          last = last.next;
      }
      return last;
  }
  ```

  性能测试分析：

  ```
  运行时间：26ms
  占用内存：9280k
  ```

+ 类似于第一种方法的变形：使用两个指针，指针A先进行遍历，当遍历到第k-1个数时，指针B开始从头遍历。当指针A到达链表尾的时候，指针B的位置就刚好为倒数第k个数。

  代码：

  ```java
  public ListNode FindKthToTail(ListNode head,int k) {
      ListNode pre = head;
      ListNode last = head;
      if(head == null || k <= 0){
          return null;
      }
      for(int i=1;i<k;i++){
          if(pre.next!=null){
              pre = pre.next;
          }else{
              return null;
          }
      }
      while(pre.next != null){
          pre = pre.next;
          last = last.next;
      }
      return last;
  }
  ```

  性能测试分析：

  ```
  运行时间：24ms
  占用内存：9552k
  ```

+ 使用堆栈。对链表进行遍历并存入堆栈中，然后再从堆栈中弹出k个元素（这种方法需要注意链表的长度是否会造成堆栈的溢出）

  代码：

  ```java
  public ListNode FindKthToTail(ListNode head,int k) {
      ListNode pre = head;
      ListNode last = null;
      int count = 0;
      Stack stack = new Stack();
      if(head == null || k <= 0){
          return null;
      }
      while(pre != null){                     
          stack.push(pre);
          pre = pre.next;
          count++;
      }
      //判断k是否超过链表长度
      if(k>count){
          return null;
      }
      for(int i =1;i<=k;i++){
          last = (ListNode) stack.pop();
      }
      return last;
  }
  ```

  测试性能分析：

  ```
  运行时间：25ms
  占用内存：9576k
  ```
