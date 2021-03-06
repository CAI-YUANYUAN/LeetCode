# 1.Two Sum[两数之和]

## 信息卡片

* 时间：2020-01-18
* 题目链接：[English](https://leetcode.com/problems/two-sum/)/[中文](https://leetcode-cn.com/problems/two-sum/)
* Tag：`Array` `Hash Table`  
## 题目描述
Given an array of integers, return indices of the two numbers such that they add up to a specific target.   
You may assume that each input would have exactly one solution, and you may not use the same element twice.   

Example:   
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].


**以下为模版

## 参考答案

### 1. 二进制方案

#### 分析

集合：和为n的可选数据集，在本题中就是可选的硬币面值：1，1，2，2，4… 以下统一称为**集合**

1. 由集合中元素的特点可以联想到 **二进制**。如果将集合中的所有元素都用二进制来表示的话：

   1 等于 2的0次方 等于 二进制的 1 
   2 等于 2的1次方 等于 二进制的 10
   4 等于 2的2次方 等于 二进制的 100
   ...
   即：
   1=2^0=(1)2; 2=2^1=(10)2; 4 = 2^2 = (100)2;..... .**（等号最后的数都是二进制表示法）**

   集合中的每一个元素都可以表示为 首位为 1 其他位为 0 的二进制数。

2. 集合中元素是成对出现的，那么可以将集合拆分为完全相同的两部分, 每一个数都可以由二进制中指定位置的1 来表示：

   8 4 2 1             —>     1 1 1 1

   8 4 2 1             —>     1 1 1 1

   那么，若目标数 n 为 11.那么  11 = 1 + 10 = 2 + 9 = 3 + 8 = 4 + 7 = 5 + 6；

   **a.** 以 **1 + 10** 为例 ： 1 的 二进制  1，  10的二进制为  1010     那么 (11) 就相当于 

   取 二进制数 第一位的1， 第四位的1 ，第2位的 1 [**从右往左**]

    即可组成 十进制的11。

   **b.** **2 + 9 = (10)2+ (1001)2** ： 取第二位的1， 第四位的1， 从第一位的1 [**从右往左**]

   同理：

   **c.** **3 + 8= (11)2+(1000)2**

   **d.** **4 + 7 = (100)2+(111)2**

   **e.** **5 + 6=(101)2+(110)2**

   > a 和 b ,c 中 其实是同一种方案。可通过**异或运算**进行去重：
   >
   > 比如，这三组方案的异或结果是相同的。1^10 == 2^9 == 3^8 == (1011)2
   >
   > d,e 也是同一种方案

#### 思路

1. 从i=0开始**(如果n=4 那么 0+4 也是一种方案，只不过只选择一个 4 而已)**，i<=(n/2), 每次i+1  循环开始：循环中将 i^(n-i)的值放到 Set（无重复元素）中
2. **最终**求 Set的 size大小。就是最终的方案数。

代码如下：

```c++
import java.util.HashSet;
import java.util.Set;

public class CoinsOfQy {

  /**测试*/
  public static void main(String[] args) {

    int n = 11;
    int result = coinsOfQy(n);
    System.out.println(result);
  }
  
  private static int coinsOfQy(int n) {

    Set<Integer> resultSet = new HashSet<>();
    for (int i =0; i<= n/2; i++){
      int r = i^(n-i);
      resultSet.add(r);
    }
    return resultSet.size();
  }
}

```


## 优秀解答

>暂缺
