# 《剑指offer》之寻找旋转数组最小值

题目：把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。 输入一个非减排序的数组的一个旋转，输出旋转数组的最小元素。 例如数组{3,4,5,1,2}为{1,2,3,4,5}的一个旋转，该数组的最小值为1。 NOTE：给出的所有元素都大于0，若数组大小为0，请返回0。

分析：当对一个**非减排序**的数组进行旋转的时候，其实得到的结果就是将该数组分为了两个部分，且第一个数组的**第一个元素**只能大于或者等于第二个数组的**最后一个元素**。所以我们可以利用二分法对旋转数组进行查找，但是我们需要注意下面这种特殊情况：

{1，0，1，1，1｝ 和 ｛1，1， 1，0，1｝ 都可以看成是递增排序数组｛0，1，1，1，1｝的旋转。

即：旋转后中间的数、最左边的、最右边的数都相同，这种情况下就没有办法使用二分法对数组进行查找了。只能使用顺序查找

补充：二分法查找实现步骤

① 首先确定整个查找区间的中间位置 mid = （min + max）/ 2 

② 用待查关键字值与中间位置的关键字值进行比较：

     i. 若相等，则查找成功；
    
    ii. 若小于，则在前半个区域继续进行折半查找；
    
    iii. 若大于，则在后半个区域继续进行折半查找；

③ 对确定的缩小区域再按折半公式，重复上述步骤。

④ 最后得到结果：要么查找成功，要么查找失败。折半查找的存储结构采用一维数组存放。



解决方案：

+ 首先对数组进行进行二分法查找，当无法使用二分法查找的时候使用顺序查找

  代码：

  ```java
  public int minNumberInRotateArray(int [] array) {
      // 判断数组是否为空
      if(array.length == 0){
          return 0;
      }
      return findMin(array);
  }
  
  private int findMin(int[] arr){
      int mid = 0;
      int left = 0;
      int right = arr.length-1;
      while(arr[left] >= arr[right]){
          if(right - left == 1){
              mid = right;
              break;
          }
          mid = (right + left) / 2;
          if(arr[left]==arr[right]&&arr[mid]==arr[left]){
              return inInOrder(arr,left,right);
          }
          if(arr[mid]>=arr[left]){
              left = mid;
          }else if(arr[mid]<=arr[right]){
              right = mid;
          }
      }
      return arr[mid];
  }
  // 顺序查找
  private static int inInOrder(int[] arr, int start, int end) {
      int min = arr[start];
      for(int i = start+1;i<=end;i++){
          if(min>arr[i]){
              min = arr[i];
          }
  
      }
      return min;
  }
  ```

  测试性能分析：

  ```
  运行时间：328ms
  占用内存：28856k
  ```




