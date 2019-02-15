# 《剑指offer》之用两个栈实现队列

题目：用两个栈来实现一个队列，完成队列的Push和Pop操作。 队列中的元素为int类型。

分析：两种数据结构的特点为

栈：先进后出

队列：先进先出

解决方案：

+ 利用两个栈，其中一个进行“入队”操作，另一个作为“出队”操作。即入队的元素都压入栈A,当需要出队的时候，就将栈A中的元素压入栈B，再将栈B中的元素弹出即可。

  代码：

  ```java
  Stack<Integer> stack1 = new Stack<Integer>();
      Stack<Integer> stack2 = new Stack<Integer>();
      // 入队操作
      public void push(int node) {
          stack1.push(node);
      }
      // 出队操作
      public int pop() {
      	// 判断"队列"是否为空
          if(stack1.empty()&&stack2.empty()){
              throw new RuntimeException("Queue is empty!");
          }
          // 如果栈B中的元素为空，则从栈A中压入元素
          if(stack2.empty()){
              while(!stack1.empty()){
                  stack2.push(stack1.pop());
              }
          }
          return stack2.pop();
      }
  ```

  测试性能分析：

  ```
  运行时间：31ms
  占用内存：9432k
  ```


