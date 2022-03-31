## 一、为什么要学希尔排序

因为简单插入排序存在一些问题

我们看简单的插入排序可能存在的问题.

数组 arr = {2,3,4,5,6,1} 这时需要插入的数 1(最小), 这样的过程是：

{2,3,4,5,6,6}

{2,3,4,5,5,6}

{2,3,4,4,5,6}

{2,3,3,4,5,6}

{2,2,3,4,5,6}

{1,2,3,4,5,6}

**结论**： 当需要插入的数是较小的数时，后移的次数明显增多，对效率有影响.

## 二、什么是希尔排序

希尔排序是希尔（Donald Shell）于1959年提出的一种排序算法。希尔排序也是一种**插入排序**，它是简单插入排序经过改进之后的一个**更高效的版本**，也称为缩小增量排序。

## 三、希尔排序的基本思想

希尔排序是把记录按下标的一定增量分组，对每组使用直接插入排序算法排序；随着增量逐渐减少，每组包含的关键词越来越多，当增量减至1时，整个文件恰被分成一组，算法便终止

> ==排序示意图==

 ![image-20220114145157872](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220114145206.png)

## 四、代码实现

> ==分步实现交换式希尔排序==

```java
/**
     * 通过交换法实现希尔排序(分步演示)
     * 思路：
     * 1、每次都要分组，即步长，初始步长是 数组长度/2(一开始基本就是两两对比交换)
     * 2、然后继续进行步长 / 2,直到步长 == 0 结束（也就排序完毕了）
     *
     * @param arr
     */
public static void shellSortBySwap1(int[] arr) {
    int temp = 0;
    // Shell排序的第一轮
    // 第一轮排序，是将10个数据分成5组（二分） 外层循环的数是比较靠后的
    for (int i = 5; i < arr.length; i++) {
        // 遍历各组中所有的元素（共5组，每组两个元素），步长为 5
        for (int j = i - 5; j >= 0; j -= 5) {
            if (arr[j + 5] < arr[j]) {
                temp = arr[j + 5];
                arr[j + 5] = arr[j];
                arr[j] = temp;
            }
        }
    }
    System.out.println("第一轮Shell排序结果：" + Arrays.toString(arr));
    // 第二轮排序
    for (int i = 2; i < arr.length; i++) {
        for (int j = i - 2; j >= 0; j -= 2) {
            if (arr[j + 2] < arr[j]) {
                temp = arr[j + 2];
                arr[j + 2] = arr[j];
                arr[j] = temp;
            }
        }
    }
    System.out.println("第二轮Shell排序结果：" + Arrays.toString(arr));
    // 第三轮排序
    for (int i = 1; i < arr.length; i++) {
        for (int j = i - 1; j >= 0; j -= 1) {
            if (arr[j + 1] < arr[j]) {
                temp = arr[j + 1];
                arr[j + 1] = arr[j];
                arr[j] = temp;
            }
        }
    }
    System.out.println("第三轮Shell排序结果：" + Arrays.toString(arr));
}
```

> ==交换式希尔排序完整代码（不推荐）==‘

交换式的希尔排序，效率很慢的（比冒泡快不了多少），所以不建议使用（尤其是数据较多的情况下）

```java
/**
     * 通过交换法实现希尔排序（完整代码）
     * 缺点：就像冒泡和选择一样会发生一些没有必要置换（即看到满足条件元素进行置换），很消耗时间
     *
     * @param arr
     */
public static void shellSortBySwap2(int[] arr) {
    int temp = 0;
    int count = 0;
    // 要再加一层循环  步长（每次内存循环结束，除2）
    for (int step = arr.length / 2; step > 0; step /= 2) {
        for (int i = step; i < arr.length; i++) {
            for (int j = i - step; j >= 0; j -= step) {
                if (arr[j] > arr[j + step]) {
                    temp = arr[j + step];
                    arr[j + step] = arr[j];
                    arr[j] = temp;
                }
            }
        }

    }
    // System.out.println("交换法希尔排序结果为：" + Arrays.toString(arr));
}
```

> ==移位式希尔排序（推荐，也是优化版）==

```java
/**
     * 希尔排序(移位法)
     * 思路: 可以参考插入排序
     */
public static void shellSortByShift(int[] arr) {
    int insertval = 0;
    int insertIndex = 0;
    // 要再加一层循环  步长（每次内存循环结束，除2）
    for (int step = arr.length / 2; step > 0; step /= 2) {
        for (int i = step; i < arr.length; i++) {
            insertval = arr[i];
            insertIndex = i;
            // 如果前面的数字比后面的大
            if (arr[insertIndex - step] > arr[insertIndex]) {
                // 这里就和插入排序很相似了
                while ((insertIndex - step) >= 0 && insertval < arr[insertIndex - step]) {
                    arr[insertIndex] = arr[insertIndex - step];
                    insertIndex -= step;
                }
                // 找到位置进行插入
                if (insertIndex != i) {
                    arr[insertIndex] = insertval;
                }
            }
        }
    }
    //        System.out.println("移位法希尔排序结果为：" + Arrays.toString(arr));
}
```

> ==速度对比==



![image-20220114161141884](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220114161143.png)
