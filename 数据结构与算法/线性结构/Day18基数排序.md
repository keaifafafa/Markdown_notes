## 一、什么是基数排序

1)[基数排序](https://baike.baidu.com/item/基数排序/7875498)（radix sort）属于“分配式排序”（distribution sort），又称“桶子法”（bucket sort）或bin sort，顾名思义，

它是通过键值的各个位的值，将要排序的[元素分配](https://baike.baidu.com/item/元素分配/2107419)至某些“桶”中，达到排序的作用

2)基数排序法是属于稳定性的排序，基数排序法的是效率高的稳定性排序法

3)基数排序(Radix Sort)是**[桶排序](http://www.cnblogs.com/skywang12345/p/3602737.html)**的扩展

4)基数排序是1887年赫尔曼·何乐礼发明的。它是这样实现的：将整数按位数切割成不同的数字，然后按每个位数分别比较。

## 二、基数排序实现思路

1)将所有待比较数值统一为同样的数位长度，数位较短的数前面补零。然后，从最低位开始，依次进行一次排序。这样从最低位排序一直到最高位排序完成以后, 数列就变成一个有序序列。

2)这样说明，比较难理解，下面我们看一个图文解释，理解基数排序的步骤

> ==图文说明==

将数组 {53, 3, 542, 748, 14, 214} 使用基数排序, 进行升序排序。

- 第一轮（个位）

   ![image-20220117201646189](https://gitee.com/lovely-hair/blog-img/raw/master/img/20220117201919.png)

- 第二轮(十位)

   ![image-20220117201709438](https://gitee.com/lovely-hair/blog-img/raw/master/img/20220117201710.png)

- 第三轮（百位）

   ![image-20220117201811537](https://gitee.com/lovely-hair/blog-img/raw/master/img/20220117201811.png)

## 三、代码实现

```java
package com.fafa.sort;

import java.util.Arrays;

/**
 * 基数排序（桶排序的扩展）
 * 其思路与桶排序还有基数排序很类似，所以这里只讲解基数排序（很消耗内存，数据量太大的时候会 OutOfMemoryError ）
 *
 * @author Sire
 * @version 1.0
 * @date 2022-01-16 20:17
 */
public class RadixSort {
    public static void main(String[] args) {
        int[] arr = {53, 3, 542, 748, 14, 214};
        radixSort(arr);
        System.out.println("基数排序结果：" + Arrays.toString(arr));
    }

    public static void radixSort(int[] arr) {
        // 创建 10 个桶（0 - 9）,每个桶就是一个一维数组
        // 为了防止在放入的时候，数据溢出，则每个一维数组（桶），大小设定为 arr.length
        int[][] bucket = new int[10][arr.length];
        // 创建10个用于统计桶内元素个数(初始值都是0,即桶内元素个数)
        int[] countBucketEle = new int[10];
        // 最大数字（用于获取最大的位数）
        int max = 0;
        // 循环遍历寻找最大数字
        for (int data : arr) {
            if (data > max) {
                max = data;
            }
        }
        // 获取最大的位数（即长度）
        int maxLength = (max + "").length();
        for (int i = 0, k = 1; i < maxLength; i++, k *= 10) {
            // 针对每个元素的对应位进行排序处理，第一次是个位，第二次是十位，第三次是百位……以此类推
            for (int j = 0; j < arr.length; j++) {
                // 获取位数（个、十、百位等）
                int digitOfElement = arr[j] / k % 10;
                // 放入对应的桶中
                bucket[digitOfElement][countBucketEle[digitOfElement]] = arr[j];
                // 对应索引加1
                countBucketEle[digitOfElement]++;
            }
            // 按照这个桶的顺序（一维数组的下标依次取出数据，放回原来的数组）
            // 原来数组的初始下标
            int index = 0;
            // 遍历 10 个桶
            for (int n = 0; n < countBucketEle.length; n++) {
                // 桶内元素不为空
                if (countBucketEle[n] != 0) {
                    for (int s = 0; s < countBucketEle[n]; s++) {
                        arr[index] = bucket[n][s];
                        index++;
                    }
                }
                // 数据置零，因为还会有其他位数的进行循环遍历
                countBucketEle[n] = 0;
            }
        }
    }
}
```

## 四、注意事项

1)基数排序是对传统桶排序的扩展，速度很快.

2)基数排序是经典的空间换时间的方式，占用内存很大, 当对海量数据排序时，容易造成 OutOfMemoryError 。

3)基数排序时稳定的。[注:假定在待排序的记录序列中，存在多个具有相同的关键字的记录，若经过排序，这些记录的相对次序保持不变，

即在原序列中，r[i]=r[j]，且r[i]在r[j]之前，而在排序后的序列中，r[i]仍在r[j]之前，**则称这种排序算法是稳定的；否则称为不稳定的**]

4)**有负数的数组，我们不用基数排序来进行排序**, **如果要支持负数，参考**: **https://code.i-harness.com/zh-CN/q/e98fa9**

> ==常用算法总结和对比==

 ![image-20220117211039227](https://gitee.com/lovely-hair/blog-img/raw/master/img/20220117211039.png)