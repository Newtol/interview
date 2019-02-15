# 《剑指offer》之二维数组查找

题目: 在一个二维数组中（每个一维数组的长度相同），每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

分析：该题目类似于一个矩阵的查找过程，每个一维数组里的元素都是逐步递增的。其中左上角的元素最小，右下角的元素最大。例如：

```java
{{1,2,8,9},{2,4,9,12},{4,7,10,13},{6,8,11,15}}
```

解决思路：

+ 方法一：通过遍历整个二维数组来判断是否存在该整数

  代码：

  ```java
  public boolean Find(int target, int [][] array){
      int rowNum = array.length;
      int columnNum = array[0].length;
      int i = 0;
      int j = 0;
      for( i = 0; i < columnNum ; i++){
      	for(j = 0; j < rowNum; j++ ){
      		if (array[j][i] == target){
      			return true;
      		}
      	}
      }
      return false;
  }
  ```

  测试结果分析:

  ```
  运行时间：181ms
  
  占用内存：17980k
  ```


+ 根据分析结果，我们发现，每行最大的数在右边，每列最大的数在最下面。所以我们从左下角从左往右搜索，当遇到比目标数大的数就往上一行继续从左往右进行搜索（因为往右的数都会比目标数大），否则就继续往右搜索，如果到达某一行的最右端仍未搜索到，则往上一行继续搜索。

  代码：

  ```java
  int rowNum = array.length;
  int columnNum = array[0].length;
  int i = 0,j=0;
  while(j < columnNum ){
      if(i == rowNum  || target < array[i][j]){
          i = 0;
          j++;
      }else if(target > array[i][j]){
          i++;
      }else if (target == array[i][j]){
          return true;
      }
  }
  return false;
  ```

  测试结果分析：

  ```
  运行时间：176ms
  
  占用内存：17668k
  ```
