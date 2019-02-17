# 《剑指offer》之调整数组顺序

题目：输入一个整数数组，实现一个函数来调整该数组中数字的顺序，使得所有的奇数位于数组的前半部分，所有的偶数位于数组的后半部分，并保证奇数和奇数，偶数和偶数之间的相对位置不变。

分析：**相对位置不变--->保持稳定性；奇数位于前面，偶数位于后面 --->存在判断，挪动元素位置；**

解决方案：

+ 使用双队列来保证顺序的不变：

  代码：

  ```java
  public void reOrderArray(int [] array) {
      Queue<Integer> queue = new LinkedBlockingQueue<>();
      Queue<Integer> queue1 = new LinkedBlockingQueue<>();
      for (int anArray : array) {
          if (anArray % 2 == 1) {
              queue.offer(anArray);
          } else {
              queue1.offer(anArray);
          }
      }
      int i =0;
      while(!queue.isEmpty()){
          array[i] = queue.poll();
          i++;
      }
      while (!queue1.isEmpty()){
          array[i]= queue1.poll();
          i++;
      }
  }
  ```

  测试性能分析：

  ```
  运行时间：20ms
  占用内存：9232k
  ```

+ 使用单队列实现：使用队列存储偶数，然后再将偶数追加至数组尾部

  代码：

  ```java
  public void reOrderArray(int [] array) {
      Queue<Integer> queue = new LinkedBlockingQueue<>();
      int count = 0;
      for (int anArray : array) {
          if (anArray % 2 == 1) {
              array[count] = anArray;
              count++;
          } else {
              queue.offer(anArray);
          }
      }
      while (!queue.isEmpty()){
          array[count] =queue.poll();
          count++;
      }
  }
  ```

  测试性能分析：

  ```java
  运行时间：18ms
  占用内存：9576k
  ```

+ 通过寻找偶数后面的第一个奇数，然后所有偶数都移动到该奇数后面。然后向后重复该过程，通过所有偶数的移动来保证稳定性。

  代码：

  ```java
  public void reOrderArray(int [] array) {
      int m = array.length;
      int k = 0;//记录已经摆好位置的奇数的个数
      for (int i = 0; i < m; i++) {
          if (array[i] % 2 == 1) {
              int j = i;
              while (j > k) {//j >= k+1
                  int tmp = array[j];
                  array[j] = array[j-1];
                  array[j-1] = tmp;
                  j--;
              }
              k++;
          }
      }
  }
  ```

  测试性能分析：

  ```
  运行时间：19ms
  占用内存：9220k
  ```


