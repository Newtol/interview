# 《剑指offer》之求数的整数次幂

题目：给定一个double类型的浮点数base和int类型的整数exponent。求base的exponent次方。

分析：求解数的次方可以使用二进制来进行计算。例如：

10^1101 = 10^0001\*10^0100\*10^1000。
即：通过&1和>>1来逐位读取1101，为1时将该位代表的乘数累乘到最终结果。

解决方案：

+ 暴力计算法：

  代码：

  ```java
  public double Power(double base, int exponent) {
      double  result=1;
      for(int i=0;i<Math.abs(exponent);i++){
          result*=base;
      }
      if(exponent<0){
          result=1/result;
      }
      return result;            
  }
  ```

  测试性能分析：

  ```
  运行时间：63ms
  占用内存：10388k
  ```

+ 二进制

  代码：

  ```java
  public double Power(double base, int n) {
      double res = 1,curr = base;
      int exponent;
      if(n>0){
          exponent = n;
      }else if(n<0){
          if(base==0)
              throw new RuntimeException("分母不能为0"); 
          exponent = -n;
      }else{// n==0
          return 1;// 0的0次方
      }
      while(exponent!=0){
          if((exponent&1)==1)
              res*=curr;
          curr*=curr;// 翻倍
          exponent>>=1;// 右移一位
      }
      return n>=0?res:(1/res);       
  }
  ```

  性能测试分析：

  ```
  运行时间：68ms
  占用内存：10432k
  ```
