# 《剑指offer》之斐波那契数列

题目：大家都知道斐波那契数列，现在要求输入一个整数n，请你输出斐波那契数列的第n项（从0开始，第0项为0）。n≤39

分析：斐波那契数列以如下被以递归的方法定义：F0=0，F1=1，Fn=Fn-1+Fn-2（n>=2，n∈N*），用文字来说，就是斐波那契数列由 0 和 1 开始，之后的斐波那契数列系数就由之前的两数相加。指的是这样一个数列：0、1、1、2、3、5、8、13、21、……

解决方案：

+ 代码：

  ```java
   public int Fibonacci(int n) {
          int first = 0;
          int last = 1;
          if(n == 0){
              return first;
          }else if(n == 1){
              return last;
          }else{
              for(int i =0;i<=n-2;i++){
                  last= first + last;
                  first = last - first;
              }
          }
          return last;
      }
  ```

  测试性能分析：

  ```
  运行时间：17ms
  占用内存：9216k
  ```

+ 使用递归实现

  代码:

  ```java
  public int Fibonacci(int n) {
      if(n==0){
          return 0;
      }else if(n==1||n==2){
          return 1;
      }else if(n==3){
          return 2;
      }else{
          return 3*Fibonacci(n-3)+2*Fibonacci(n-4);
      }
          
  }
  ```

  测试性能分析：

  ```java
  运行时间：25ms
  占用内存：9340k
  ```


