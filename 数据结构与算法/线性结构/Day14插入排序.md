 

## 一、插入排序简介

> ==介绍==

插入排序属于内部排序算法，是对预排序的元素以插入的方式找寻该元素的适当位置，以达到排序的目的。

> ==排序思想==

插入排序（Insertion Sorting）的**基本思想**是：

把n个待排序的元素看成为一个有序表和一个无序表，开始时有序表中只包含一个元素，无序表中包含有n-1个元素，

排序过程中每次从无序表中取出第一个元素，把它的排序码依次与有序表元素的排序码进行比较，将它插入到有序表中的适当位置，使之成为新的有序表。

> ==思路图==

 ![image-20220113133356188](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220113133406.png)

## 二、具体实现及优化（小优化）

> ==流程演示==

本来的顺序是 

```java
{101, 34, 119, 1}
```

- 第一轮遍历过程及结果

   ![image-20220113135153133](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220113135153.png)

- 第二轮遍历过程及结果

   ![image-20220113135425364](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220113135425.png)

- 第三轮遍历过程及结果

    ![image-20220113141451323](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220113141451.png)

提示： 由于默认第一个元素是有序的，所以只需要遍历 （数组长度 - 1）次即可！

> ==代码实现==

```java
// 这边是升序的一个思路
// 因为默认第一个是有序的，所以从第二个开始遍历（所以下标从1开始）
for(int i = 1; i < arr.length; i++){
    // 先保留需要插入的值，后面会用到
    int insertVal = arr[i];
    // 前一个位置（因为每次都是和前一个位置作比较的）
    int insertIndex = i - 1;
    while(insertIndex >= 0 && insertVal < arr[insertIndex]){
        // 可以理解为把大数后移了
        arr[insertIndex + 1] = arr[insertIndex];
        // 继续向前寻找（知道找到最小的）
        insertIndex--;
    }
    // 小优化（避免本身就是有序的情况还要进行赋值，浪费时间）
    if((insertIndex + 1) != i){
        // 将最小值（也就是需要插入的值）赋值到目标位置
        arr[insertIndex] = insertVal;
    }
}
```

> ==测试一下执行效率==

```java
/**
     * 测试插入排序
     */
@Test
public void testInsert() {
    // 容量
    int capacity = 80000;
    // 创建 8W 容量的数组
    int[] arr = new int[capacity];
    // 初始化数据
    for (int i = 0; i < capacity; i++) {
        // 生成随机数
        arr[i] = (int) (Math.random() * (capacity * 100));
    }
    SimpleDateFormat sd = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
    // 开始时间
    String start = sd.format(new Date());
    System.out.println("排序前的时间" + start);
    // 插入排序
    InsertSort.insertSort(arr);
    String end = sd.format(new Date());
    System.out.println("排序后的时间" + end);
    //        System.out.println(Arrays.toString(arr));
}

```

 ![image-20220113140855618](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220113140855.png)

效果很好，符合图中所说的特点

 ![image-20220113141017657](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220113141017.png)
