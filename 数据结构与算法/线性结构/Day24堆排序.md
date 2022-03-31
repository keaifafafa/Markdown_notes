## 一、什么是堆排序

> ==简介==

 ![image-20220126212911264](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220126212921.png)

> ==基本思想==

 ![image-20220126212937223](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220126212937.png)

## 二、堆排序步骤演示

> ==**步骤一 构造初始堆。将给定无序序列构造成一个大顶堆（一般升序采用大顶堆，降序采用小顶堆)。**==

1) .假设给定无序序列结构如下

 ![IMG_256](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220126213350.gif)

2) .此时我们从最后一个非叶子结点开始（叶结点自然不用调整，第一个非叶子结点 arr.length/2-1=5/2-1=1，也就是下面的6结点），从左至右，从下至上进行调整。

 ![IMG_257](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220126213349.gif)

3) .找到第二个非叶节点4，由于[4,9,8]中9元素最大，4和9交换。

 ![IMG_258](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220126213347.gif)

4) 这时，交换导致了子根[4,5,6]结构混乱，继续调整，[4,5,6]中6最大，交换4和6。

 ![IMG_259](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220126213338.gif)

此时，我们就将一个无序序列构造成了一个大顶堆。

> ==**步骤二 将堆顶元素与末尾元素进行交换，使末尾元素最大。然后继续调整堆，再将堆顶元素与末尾元素交换，得到第二大元素。如此反复进行交换、重建、交换。**==

1) .将堆顶元素9和末尾元素4进行交换

 ![IMG_260](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220126213244.gif)

2) .重新调整结构，使其继续满足堆定义

 ![image-20220126214338652](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220126214338.png)

3) .再将堆顶元素8与末尾元素5进行交换，得到第二大元素8.

 ![image-20220126214359572](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220126214359.png)

4) 后续过程，继续进行调整，交换，如此反复进行，最终使得整个序列有序

 ![IMG_263](https://fafa-blog-img.oss-cn-beijing.aliyuncs.com/images/img/20220126213237.gif)

**再简单总结下堆排序的基本思路：**

1. **将无序序列构建成一个堆，根据升序降序需求选择大顶堆或小顶堆;**
2. **将堆顶元素与末尾元素交换，将最大元素"沉"到数组末端;**
3. **重新调整结构，使其满足堆定义，然后继续交换堆顶元素与当前末尾元素，反复执行调整+交换步骤，直到整个序列有序。**

## 三、具体代码实现

> 实验数据与上图一致

```java
package com.fafa.tree;

import java.util.Arrays;

/**
 * 堆排序
 *
 * @author Sire
 * @version 1.0
 * @date 2022-01-25 17:05
 */
public class HeapSort {
    public static void main(String[] args) {
        int[] arr = {4, 6, 8, 5, 9, 77, 89, 100, -1, -99, -56};
        // 第一轮测试
        //adjustHeap(arr, 1, arr.length);
        //System.out.println(Arrays.toString(arr));
        // 第二轮测试
        //adjustHeap(arr, 0, arr.length);
        //System.out.println(Arrays.toString(arr));
        // 完整测试
        heapSort(arr);
    }

    /**
     * 堆排序
     *
     * @param arr 待排序树组
     */
    public static void heapSort(int[] arr) {
        int length = arr.length;
        int temp = 0;
        // 1、将无序序列构建成一个堆，根据升降序需求选择大顶堆或小顶堆
        for (int i = length / 2 - 1; i >= 0; i--) {
            adjustHeap(arr, i, length);
        }

        /**
         * 2、将堆顶元素与末尾元素交换，将最大元素 “沉” 到数组末端；
         * 3、重新调整结构，使其满足堆定义，然后继续交换堆顶元素与当前的末尾元素，反复执行调整 + 交换步骤，直到整个序列有序
         *
         */
        for (int j = length - 1; j > 0; j--) {
            // 交换
            temp = arr[j];
            arr[j] = arr[0];
            arr[0] = temp;
            // 重新调整堆 寻找新的最大的元素
            adjustHeap(arr, 0, j);
        }

    }

    /**
     * 调整成大小堆（这里以大堆为例）
     * 说明：
     * 1、调整顺序是从左向右，从下到上的顺序
     *
     * @param arr    待排序树组
     * @param i      待调整的父节点下标
     * @param length 数组的长度
     */
    public static void adjustHeap(int[] arr, int i, int length) {
        // 保留父节点元素
        int temp = arr[i];
        // 2 * i + 1 代表 i 的左子节点，同理， k * 2 + 1 代表 k 的左子节点
        for (int k = 2 * i + 1; k < length; k = k * 2 + 1) {
            // 寻找左右节点中比较大的一个
            // k + 1 < length 是为了避免无右节点的情况，避免不必要的对比（提高效率）
            if (k + 1 < length && arr[k] < arr[k + 1]) {
                // 因为左节点小于右节点，所以需要移动k，将其移动到右节点的位置
                k++;
            }
            // 和父节点对比大小
            // 这里一定要写temp，因为不会只比较一次
            if (arr[k] > temp) {
                arr[i] = arr[k];
                // 便于接下来的对比（后面的节点，假设在第一层试试）
                i = k;
            } else {
                break;
            }
        }
        // 将原父节点的值 赋值给 新的 arr[i]
        arr[i] = temp;
    }
}

```

 

