## 一、线性查找

> ==思路==

很简单，就是遍历一遍然后从中比对

> ==代码实现==

```java
package com.fafa.search;

import java.util.ArrayList;
import java.util.List;

/**
 * 线性查找
 *
 * @author Sire
 * @version 1.0
 * @date 2022-01-18 14:14
 */
public class SeqSearch {
    public static void main(String[] args) {
        int[] arr = {19, 33, 45, 67, 2, 53, 99, 88, 1, 2, 100};
        int target = 55;
        List<Integer> seqSearch = seqSearch(arr, target);
        System.out.println(seqSearch.toString());
    }

    /**
     * 返回数组内目标元素的下标（可能含有多个）
     *
     * @param arr
     * @param target
     * @return
     */
    public static List<Integer> seqSearch(int[] arr, int target) {
        List<Integer> list = new ArrayList<>();
        for (int i = 0; i < arr.length; i++) {
            if (arr[i] == target) {
                // 添加下标
                list.add(i);
            }
        }
        return list;
    }
}

```

## 二、二分查找（递归法）

> ==思路==

   * 思路：
     * 1、先计算出中间的下标，并保留中间下标对应的数字
     * 2、然后递归查找，如果目标比中间值小，那么向左递归，反之，向右递归
     * 3、如果找到返回其下标，未找到则继续递归，直到 left > right 为止

> ==代码实现==

```java
package com.fafa.search;

import java.util.ArrayList;
import java.util.List;

/**
 * 二分查找(数组一定要是有序的)
 *
 * @author Sire
 * @version 1.0
 * @date 2022-01-18 14:32
 */
public class BinarySearch {
    public static void main(String[] args) {
        //        int[] arr = {1, 2, 3, 8, 8, 8, 8, 8, 8, 9, 10, 89, 1000, 1234};
        int[] arr = {1, 9, 10, 89, 1000, 1000, 1234};
        int target = 1000;
        // 方法一
        /* int res = binarySearch01(arr, 0, arr.length - 1, target);
        System.out.println("res = " + res);*/

        // 方法二
        List<Integer> list = binarySearch02(arr, 0, arr.length - 1, target);
        System.out.println("list = " + list.toString());

    }

    /**
     * 二分查找基础方法（只能找到一个）
     * 递归法
     * 思路：
     * 1、先计算出中间的下标，并保留中间下标对应的数字
     * 2、然后递归查找，如果目标比中间值小，那么向左递归，反之，向右递归
     * 3、如果找到返回其下标，未找到则继续递归，直到 left > right 为止
     *
     * @param arr
     * @param left
     * @param right
     * @param target
     * @return
     */
    public static int binarySearch01(int[] arr, int left, int right, int target) {
        // 递归头（结束标志）
        if (left > right) {
            return -1;
        }
        // 中值下标
        int midIndex = (left + right) / 2;
        // 中值
        int midVal = arr[midIndex];

        // 向左递归
        if (target < midVal) {
            return binarySearch01(arr, left, midIndex - 1, target);
        }
        // 向右递归
        else if (target > midVal) {
            return binarySearch01(arr, midIndex + 1, right, target);
        }
        // 找到目标
        else {
            return midIndex;
        }
    }

    /**
     * 二分查找基础方法（可以找到多个）
     * 递归法
     * 思路：
     * 1、在收到目标后，不要马上返回，而是先扫描其左边的（因为是有序的）
     * 2、如果左边的下标小于0 或者 不等于目标值了，则直接结束，否则将找到下标添加到集合中
     * 3、添加目标的下标
     * 4、扫描目标右面的元素，方法和左边的类似
     * 5、全部扫完，返回即可
     *
     * @param arr
     * @param left
     * @param right
     * @param target
     * @return
     */
    public static List<Integer> binarySearch02(int[] arr, int left, int right, int target) {
        // 递归头（结束标志）
        if (left > right) {
            return new ArrayList<Integer>();
        }
        // 中值下标
        int midIndex = (left + right) / 2;
        // 中值
        int midVal = arr[midIndex];

        // 向左递归
        if (target < midVal) {
            return binarySearch02(arr, left, midIndex - 1, target);
        }
        // 向右递归
        else if (target > midVal) {
            return binarySearch02(arr, midIndex + 1, right, target);
        }
        // 找到目标
        else {
            // 下标集合（用于接受多个目标元素的下标）
            List<Integer> list = new ArrayList<Integer>();
            // 用于遍历下标
            int listIndex = midIndex - 1;
            // 先扫描左边的
            while (listIndex >= left) {
                if (arr[listIndex] == midVal) {
                    list.add(listIndex);
                    listIndex--;
                } else {
                    break;
                }
            }
            list.add(midIndex);
            // 扫描右边
            listIndex = midIndex + 1;
            while (listIndex <= right) {
                if (arr[listIndex] == midVal) {
                    list.add(listIndex);
                    listIndex++;
                } else {
                    break;
                }
            }
            return list;
        }
    }
}

```

## 三、插值查找

> ==原理介绍==

 ![image-20220118223816552](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220121153743.png)

> ==代码实现==

```java
package com.fafa.search;

/**
 * 插值查找
 *
 * @author Sire
 * @version 1.0
 * @date 2022-01-18 21:51
 */
public class InsertValSearch {
    public static void main(String[] args) {
        int[] arr = new int[100];
        // 生成100个连续的测试数组（1-100）
        for (int i = 0; i < arr.length; i++) {
            arr[i] = i + 1;
        }
        int target = 66;
        // 调用插值查找
        int search = insertValSearch(arr, 0, arr.length - 1, target);
        System.out.println("插值查找结果：" + search);

    }

    /**
     * 插值查找
     * 其思路与二分查找很类似
     * 不同之处是： 定位midIndex的公式不同（自适应的算法）
     * 算法公式是： int midIndex = left + (right - left) * (target - arr[left]) / (arr[right] - arr[left]);
     *
     * @param arr
     * @param left
     * @param right
     * @param target
     * @return
     */
    public static int insertValSearch(int[] arr, int left, int right, int target) {
        System.out.println("insertValSearch被调用~");
        // 新增了两条，需要对target的合法性进行校验，因为自适应公式用到了target值（所以必须要做校验）
        if (left > right || target < arr[left] || target > arr[right]) {
            return -1;
        }
        // 自适应公式
        int midIndex = left + (right - left) * (target - arr[left]) / (arr[right] - arr[left]);
        int midVal = arr[midIndex];
        if (target > midVal) {
            return insertValSearch(arr, midIndex + 1, right, target);
        } else if (target < midVal) {
            return insertValSearch(arr, left, midIndex - 1, target);
        } else {
            return midIndex;
        }
    }
}

```

> ==注意事项==

1)对于数据量较大，**关键字分布比较均匀**的查找表来说，采用**插值查找**, **速度较快**.

2)关键字分布不均匀的情况下，该方法不一定比折半查找要好



## 四、斐波那契查找

> ==简介==

**注意：斐波那契算法也是需要数组是有序的！！！**

 ![image-20220120210839297](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220120210848.png)

> ==算法思路==

 ![image-20220120210926843](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220120210926.png)

> ==代码实现==

```java
package com.fafa.search;

import java.util.Arrays;

/**
 * 斐波那契查找
 *
 * @author Sire
 * @version 1.0
 * @date 2022-01-19 18:11
 */
public class FibonacciSearch {
    /**
     * 最大容量
     */
    private static int maxSize = 20;

    public static void main(String[] args) {
        int[] arr = {1, 8, 10, 189, 1000, 1234};
        System.out.println("index = " + fibSearch(arr, 1234));
    }

    /**
     * 生成斐波那契数列
     *
     * @return
     */
    public static int[] fibonacci() {
        int[] nums = new int[maxSize];
        for (int i = 0; i < maxSize; i++) {
            if (i == 0 || i == 1) {
                nums[i] = 1;
            } else {
                nums[i] = nums[i - 1] + nums[i - 2];
            }
        }
        return nums;
    }

    /**
     * 斐波那契查找（迭代法）
     *
     * @param arr 数组
     * @param key 我们需要查找的关键值
     * @return 返回对应的下标，如果没有，返回 -1
     */
    public static int fibSearch(int[] arr, int key) {
        int low = 0;
        int high = arr.length - 1;
        // 存放mid值
        int mid = 0;
        // 生成斐波那契额数组
        int[] f = fibonacci();
        // 表示斐波那契数值的下标
        int k = 0;
        // 获取斐波那契分割数值的下标（只要顺序表长度为 f[k] - 1 ， 即可以使用mid公式）
        while (high > f[k] - 1) {
            k++;
        }
        // 因为 f[k] 值 可能大于 a 的 长度，因此我们需要使用Arrays类，构造一个新的数组，并指向temp[]
        // 不足的部分会使用0填充
        int[] temp = Arrays.copyOf(arr, f[k]);
        //实际上需求使用a数组最后的数填充 temp
        //举例:
        //temp = {1,8, 10, 89, 1000, 1234, 0, 0}  => {1,8, 10, 89, 1000, 1234, 1234, 1234,}
        for (int i = k; i < temp.length; i++) {
            temp[i] = arr[high];
        }

        while (low <= high) {
            mid = low + f[k - 1] - 1;
            // 需要继续往前找（可以理解为向左）
            if (key < temp[mid]) {
                high = mid - 1;
                // 注意：这里为什么是k--;
                // 1、全部元素 = 前面元素 + 后面元素
                // 2、f[k] = f[k -1] + f[k - 2];
                // 因为 前面有 f[k - 1]个元素,所以可以继续拆分 f[k - 1] = f[k - 2] + f[k - 3]
                // 即 在 f[k - 1] 的前面继续查找 k--
                // 即下次循环 mid = f[k - 1 - 1] - 1
                k--;
            } else if (key > temp[mid]) {
                low = mid + 1;
                //为什么是k -=2
                //说明
                //1. 全部元素 = 前面的元素 + 后边元素
                //2. f[k] = f[k - 1] + f[k - 2]
                //3. 因为后面我们有f[k - 2] 所以可以继续拆分 f[k - 2] = f[k-3] + f[k-4]
                //4. 即在f[k - 2] 的前面进行查找 k -= 2
                //5. 即下次循环 mid = f[k - 1 - 2] - 1
                k -= 2;
            } else {
                // 要返回比较小的一个（因为mid，可能会指向扩容的地址）
                return mid = mid <= high ? mid : high;
            }
        }
        return -1;
    }
}

```

