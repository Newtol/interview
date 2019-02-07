# 从尾到头打印链表

题目：输入一个链表，按链表值从尾到头的顺序返回一个ArrayList

分析：将一个链表进行逆序。

解决思路：

+ 使用两个链表：一个用来存放传进来的数据，一个用于存放逆序后的列表。

  代码：

  ```java
  public ArrayList<Integer> printListFromTailToHead(ListNode listNode) {
      ArrayList<Integer> list = new ArrayList<Integer>();
      ArrayList<Integer> result = new ArrayList<Integer>();
      while ( listNode != null ) {
          list.add( listNode.val );
          listNode = listNode.next;
      }
      for ( int i = list.size()-1; i>=0; i-- ) {
          result.add( list.get(i) );
      }
      return result;
  }
  
  ```

  测试性能分析:

  ```
  运行时间：22ms
  占用内存：9380k
  ```

+ 使用单个链表：先对数据进行存放后，将链表进行逆序（第i个数据和len-1-i个数据进行交换）

  代码：

  ```java
  public ArrayList<Integer> printListFromTailToHead(ListNode listNode) {
      ArrayList<Integer> list = new ArrayList<Integer>();
      Integer temp;
      while ( listNode != null ) {
          list.add( listNode.val );
          listNode = listNode.next;
      }
      int len = list.size();
      for ( int i =0; i < len/2  ; i++ ) {
          temp = list.get(i);
          list.set(i,list.get(len - 1 - i));
          list.set(len-1-i,temp);
      }
      return list;
  }
  ```

  测试性能分析:

  ```
  运行时间：25ms
  占用内存：9376k
  ```

+ 使用堆栈：利用堆栈“先进后出”的特点，对传入的数据进行存放，然后再依次弹出堆栈中的元素到链表中，实现逆序

  代码：

  ```java
  public ArrayList<Integer> printListFromTailToHead(ListNode listNode) {
      Stack<Integer> stack = new Stack<Integer>();
      ArrayList<Integer> list = new ArrayList<Integer>();
      while ( listNode != null ) {
          stack.push(listNode.val);
          listNode = listNode.next;
      }
      if (!stack.isEmpty()) {
          list.add(stack.pop());
      }
      return list;
  }
  ```

  测试性能分析：

  ```
  运行时间：22ms
  占用内存：9304k
  ```

+ 通过递归实现（参考）：通过递归对链表中的元素进行逆序。

  代码：

  ```java
  public class Solution {
      ArrayList<Integer> arrayList=new ArrayList<Integer>();
      public ArrayList<Integer> printListFromTailToHead(ListNode listNode) {
          if(listNode!=null){
              printListFromTailToHead(listNode.next);
              arrayList.add(listNode.val);
          }
          return arrayList;
      }
  }
  ```

  测试性能分析:

  ```
  运行时间：18ms
  占用内存：9256k
  ```




