# 《剑指offer》之字符串替换

题目：请实现一个函数，将一个字符串中的每个空格替换成“%20”。例如，当字符串为We Are Happy.则经过替换之后的字符串为We%20Are%20Happy。

解题方案:

+ 使用replace()函数：通过将StringBuffer转换为String类，然后使用自带的replace函数进行字符替代。

  代码：

  ```java
  public String replaceSpace(StringBuffer str) {
      return str.toString().replace(" ","%20");	
  }
  ```

  测试性能分析：

  ```
  运行时间：23ms
  占用内存：9464k
  ```

+ 遍历字符串: 通过遍历字符串，如果为空格，则在新的字符串后面追加“%20”，否则就将该字符串追加到新的字符串后面。 

  代码：

  ```java
  public String replaceSpace(StringBuffer str) {
  	StringBuilder stringBuilder = new StringBuilder();
  	char[] charArr = str.toString().toCharArray();
  	for (char aCharArr : charArr) {
  		if (!Character.isSpaceChar(aCharArr)) {
  			stringBuilder.append(aCharArr);
  		} else {
  			stringBuilder.append("%20");
  		}
  	}
  	return stringBuilder.toString();	
  }
  ```

  测试性能分析：

  ```
  运行时间：22ms
  占用内存：9576k
  ```

+ 遍历字符串2：通过charAt()函数对于字符串进行遍历。

  代码：

  ```java
  public String replaceSpace(StringBuffer str) {
      StringBuilder stringBuilder = new StringBuilder();
      for(int i = 0;i < str.length();i++ ){
          if(Character.isSpaceChar(str.charAt(i))){
              stringBuilder.append("%20");
          }else {
              stringBuilder.append(str.charAt(i));
          }
      }
      return stringBuilder.toString();	
  }
  ```

  测试性能分析：

  ```
  运行时间：23ms
  占用内存：9672k
  ```
