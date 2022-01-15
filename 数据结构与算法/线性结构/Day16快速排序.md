## 一、什么是快速排序

**快速排序（**Quicksort**）是对冒泡排序的一种改进。**基本思想**是：通过一趟排序将要排序的数据分割成独立的两部分，其中一部分的所有数据都比另外一部分的所有数据都要小，然后再按此方法对这两部分数据分别进行快速排序，整个排序过程可以递归进行，以此达到整个数据变成有序序列**

效率上来讲，一般情况下是和希尔排序差不多的（结尾有对比图，快速排序更适合数据量大的情况下使用，越大越能体现其优势），当然快排的快是以空间换时间得来的（递归）。

## 二、快速排序示意图

 ![image-20220114222059401](https://gitee.com/lovely-hair/blog-img/raw/master/img/20220114222100.png)

 ![image-20220114222221135](https://gitee.com/lovely-hair/blog-img/raw/master/img/20220114222221.png)

## 三、代码实现

```java
package com.fafa.sort;

import java.util.Arrays;

/**
 * 快速排序
 *
 * @author Sire
 * @version 1.0
 * @date 2022-01-14 18:16
 */
public class QuickSort {
    public static void main(String[] args) {
        //        int[] arr = {-9, 78, 1, 0, 0, -3, 23, -567, 70, -10, 99, 108, 4, -55};
        //        int[] arr = {-9, 78, 1, -92, 0, -3, 23, -567, 70};
        //        int[] arr = {-9, 78, 1, 0, 0, -3, 23, -567, 70};
        int[] arr = {3, -1};
        quickSort(arr, 0, arr.length - 1);
        System.out.println(Arrays.toString(arr));
    }

    /**
     * 快速排序实现（用空间换时间）
     *
     * @param arr
     */
    public static void quickSort(int[] arr, int left, int right) {
        // 左索引
        int l = left;
        // 右索引
        int r = right;
        // 中轴值
        int pivot = arr[(l + r) / 2];
        int temp = 0;
        // 其实while循环结束后， l == r
        while (l < r) {
            // 寻找左边比 中轴值大的
            while (arr[l] < pivot) {
                l++;
            }
            // 寻找右边比 中轴值小的
            while (arr[r] > pivot) {
                r--;
            }
            // 如果 l >= r,说明pivot的左右两边的值，已经按照左边全部是小于等于pivot值，右边全部是大于等于pivot的值
            // 这一步不加的话，后面的递归会栈溢出
            // 避免 l == r 的情况，因为下面还有两条if语句（对 l 和 r进行重置）
            if (l == r) {
                break;
            }
            // 交换
            temp = arr[l];
            arr[l] = arr[r];
            arr[r] = temp;
            // 如果arr[l] == pivot的话,直接 r--；是其不满足 l < r 的条件，直接跳出循环结束本次
            if (arr[l] == pivot) {
                r--;
            }
            // 如果arr[r] == pivot的话,直接 l++；是其不满足 l < r 的条件，直接跳出循环结束本次
            if (arr[r] == pivot) {
                l++;
            }
        }
        // 接下来就是递归操作了
        // 如果 l == r，否则是个死循环（栈溢出Stack Overflow），最典型的例子就是 l 和 r 都在 pivot 的位置
        if (l == r) {
            // 左指针右移一下
            l++;
            // 右指针左移一下
            r--;
        }
        // 向左递归（因为右指针还未到最左边）
        if (left < r) {
            quickSort(arr, left, r);
        }
        // 右递归 (同上)
        if (right > l) {
            quickSort(arr, l, right);
        }
    }
}

```

## 四、总结

**当然这还不是最优的快速排序，不过已经是优化过得了，如果想要更快的话，可以试试随机快速排序（即每次选的不是中间的值）**

随机快速排序代码( letcode 官方测试这个是 **2ms**，上面那个是 **8 ms**【个人感觉第一种就够用了】)

**[letcode相关题型传送门](https://leetcode-cn.com/problems/sort-an-array/solution/pai-xu-shu-zu-by-leetcode-solution/)**

```java
class Solution {
    public int[] sortArray(int[] nums) {
        randomizedQuicksort(nums, 0, nums.length - 1);
        return nums;
    }

    public void randomizedQuicksort(int[] nums, int l, int r) {
        if (l < r) {
            int pos = randomizedPartition(nums, l, r);
            randomizedQuicksort(nums, l, pos - 1);
            randomizedQuicksort(nums, pos + 1, r);
        }
    }

    public int randomizedPartition(int[] nums, int l, int r) {
        int i = new Random().nextInt(r - l + 1) + l; // 随机选一个作为我们的主元
        swap(nums, r, i);
        return partition(nums, l, r);
    }

    public int partition(int[] nums, int l, int r) {
        int pivot = nums[r];
        int i = l - 1;
        for (int j = l; j <= r - 1; ++j) {
            if (nums[j] <= pivot) {
                i = i + 1;
                swap(nums, i, j);
            }
        }
        swap(nums, i + 1, r);
        return i + 1;
    }

    private void swap(int[] nums, int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
}
```

> ==和希尔排序速度对比（数据来自上面的letcode试题测试）==

 ![image-20220115152902347](https://gitee.com/lovely-hair/blog-img/raw/master/img/20220115152910.png)

