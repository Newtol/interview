# 《剑指offer》之跳台阶及变态跳台阶

题目：一只青蛙一次可以跳上1级台阶，也可以跳上2级。求该青蛙跳上一个n级的台阶总共有多少种跳法（先后次序不同算不同的结果）。

分析：当n=1时，有1种方式；当n=2时，有2种方式；当n=3时，有3种方式；当n=4时，有5种方式...可知，跳台阶其实是符合**斐波那契数列**的。即当n阶时，共有f(n-1)+f(n-2)种方式。

解决方案：

+ 采用**斐波那契数列**数列实现：

  代码：

  ```java
   public int JumpFloor(int target) {
          int first = 0;
          int last = 1;
          if(target == 0){
              return first;
          }else if(target == 1){
              return last;
          }else{
              for(int i =0;i<=target-1;i++){
                  last= first + last;
                  first = last - first;
              }
          }
  
  
          return last;
      }
  ```

  测试性能分析：

  ```
  运行时间：16ms
  占用内存：9220k
  ```



题目：一只青蛙一次可以跳上1级台阶，也可以跳上2级……它也可以跳上n级。求该青蛙跳上一个n级的台阶总共有多少种跳法。

分析：

因为n级台阶，第一步有n种跳法：跳1级、跳2级、到跳n级

 跳1级，剩下n-1级，则剩下跳法是f(n-1)

 跳2级，剩下n-2级，则剩下跳法是f(n-2)

 所以f(n)=f(n-1)+f(n-2)+...+f(1)

 因为f(n-1)=f(n-2)+f(n-3)+...+f(1)

  所以f(n)=2*f(n-1)

解决方案:

+ 使用递归实现：

  代码：

  ```java
  public int JumpFloorII(int target) {
      if (target == 0){
          return 1;
      }else if(target == 1){
          return 1;
      }else {
          return 2*JumpFloorII(target-1);
      }
  }
  ```

  测试性能分析：

  ```
  运行时间：19ms
  占用内存：9180k
  ```


